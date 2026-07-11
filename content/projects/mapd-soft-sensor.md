---
title: "Reliability-Aware Inferential Measurement for MAPD Hydrogenation Control"
date: 2026-01-15T00:00:00Z
draft: false
description: "A soft sensor reframed as a reliability-aware measurement layer that decides when to trust the analyzer, when to rely on the model, and when to fall back — evaluated on a year of industrial reactor data."
tags: ["Soft Sensors", "Uncertainty Quantification", "Process Control", "Machine Learning"]
categories: ["Projects"]
---

Selective hydrogenation units remove trace methylacetylene and propadiene
(MAPD) from a propylene stream. The more selective way to dose hydrogen is to
ratio it against the measured inlet MAPD concentration — but that requires a
continuous, trustworthy MAPD signal at every control interval, and the online
gas chromatograph (GC) that provides it is intermittent and occasionally
unreliable.

The central observation of this work is that a soft sensor for closed-loop use
cannot be judged as a standalone predictor. Low aggregate error and near-nominal
interval coverage can still hide local reliability loss during operating-state
transitions — exactly when a controller can least afford a bad measurement. So
the soft sensor is treated instead as part of a *reliability-aware measurement
layer* that decides, at each step, whether to trust the analyzer, rely on the
model, or route the controller to a conservative fallback.

{{< figure src="/projects/mapd-architecture.png" align="center" width="600" alt="Three-stage inferential-measurement architecture: interval-valued soft sensor, analyzer validation and bias correction, then fusion or fallback." caption="The three-stage architecture: an interval-valued soft sensor, analyzer validation with bias correction, and a fusion-or-fallback stage that emits both a continuous measurement and a status flag identifying the active source." >}}

**Approach**

- **Interval-valued prediction.** A temporal convolutional network with
  MC-dropout and split-conformal calibration emits a value *and* a prediction
  interval — the interval width becomes an operational reliability signal.
- **Analyzer validation and bias correction.** Incoming GC readings are
  validated and fused through a robust bias filter rather than trusted blindly.
- **Source selection with fallback.** An operating-domain monitor adds a
  representativeness check; when neither the analyzer nor the model is eligible,
  the layer falls back conservatively and flags the active source.

The method is evaluated on one year of industrial reactor historian data with
chronological holdout testing and GC-withholding windows that emulate extended
analyzer outages. Among the models compared, the conformally calibrated TCN gave
the best balance of accuracy and empirical coverage.

{{< figure src="/projects/mapd-reactor-pfd.png" align="center" width="480" alt="Process flow diagram of the selective MAPD hydrogenation section, showing the hydrogen feed, lead/lag fixed-bed reactors, and analyzer locations." caption="The selective hydrogenation section: hydrogen is dosed into the depropanizer overhead feed ahead of lead/lag fixed-bed reactors, with analyzers on the reactor inlet and outlet." >}}

The broader point is a reframing: soft sensing for analyzer-dependent control is
a *deployment* problem in which prediction accuracy and online measurement
reliability have to be assessed together, before the estimate is ever allowed to
move a valve.

---

*Manuscript submitted to the* Journal of Process Control *(2026).*
