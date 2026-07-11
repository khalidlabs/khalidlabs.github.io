---
title: "Reliability-Aware Inferential Measurement for MAPD Hydrogenation Control"
date: 2026-01-07T00:00:00Z
draft: false
description: "A soft sensor built as a reliability-aware measurement layer that decides when to trust the analyzer, when to rely on the model, and when to fall back. Evaluated on a year of industrial reactor data."
tags: ["Soft Sensors", "Uncertainty Quantification", "Process Control", "Machine Learning"]
categories: ["Projects"]
---

Selective hydrogenation units remove trace methylacetylene and propadiene
(MAPD) from a propylene stream. The more selective way to dose hydrogen is to
ratio it against the measured inlet MAPD concentration. That strategy requires
a continuous and trustworthy MAPD signal at every control interval, and the
online gas chromatograph (GC) that provides it is intermittent and occasionally
unreliable.

A soft sensor intended for closed-loop use cannot be judged as a standalone
predictor. Low aggregate error and near-nominal interval coverage can still
hide local reliability loss during operating-state transitions, which is
exactly when a controller can least afford a bad measurement. The soft sensor
is therefore treated as part of a reliability-aware measurement layer that
decides, at each step, whether to trust the analyzer, rely on the model, or
route the controller to a conservative fallback.

{{< figure src="/projects/mapd-architecture.png" align="center" width="600" alt="Three-stage inferential-measurement architecture with an interval-valued soft sensor, analyzer validation and bias correction, and fusion or fallback." caption="The three-stage architecture. An interval-valued soft sensor, analyzer validation with bias correction, and a fusion-or-fallback stage that emits a continuous measurement together with a status flag identifying the active source." >}}

**Approach**

- **Interval-valued prediction.** A temporal convolutional network with
  MC-dropout and split-conformal calibration emits a value and a prediction
  interval. The interval width serves as an operational reliability signal.
- **Analyzer validation and bias correction.** Incoming GC readings are
  validated and fused through a robust bias filter rather than trusted blindly.
- **Source selection with fallback.** An operating-domain monitor adds a
  representativeness check. When neither the analyzer nor the model is
  eligible, the layer falls back conservatively and flags the active source.

The method is evaluated on one year of industrial reactor historian data with
chronological holdout testing and GC-withholding windows that emulate extended
analyzer outages. Among the models compared, the conformally calibrated TCN
gave the best balance of accuracy and empirical coverage.

{{< figure src="/projects/mapd-reactor-pfd.png" align="center" width="480" alt="Process flow diagram of the selective MAPD hydrogenation section, showing the hydrogen feed, lead and lag fixed-bed reactors, and analyzer locations." caption="The selective hydrogenation section. Hydrogen is dosed into the depropanizer overhead feed ahead of lead and lag fixed-bed reactors, with analyzers on the reactor inlet and outlet." >}}

Soft sensing for analyzer-dependent control is a deployment problem. Prediction
accuracy and online measurement reliability must be assessed together before
the estimate is allowed to move a valve.

---

*Manuscript submitted to the* Journal of Process Control *(2026).*
