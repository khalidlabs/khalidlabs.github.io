---
title: "Large Reasoning Models for Abnormal Situation Management"
date: 2026-06-11T00:00:00Z
draft: false
description: "A general-purpose large reasoning model acting as a guarded supervisory layer that manages abnormal situations on an industrial plant through a bounded, programmatically verified action interface."
tags: ["Large Reasoning Models", "Process Safety", "Autonomy", "Control Systems"]
categories: ["Projects"]
---

Automation runs safety-critical processes well inside their design envelope.
Abnormal situations still fall to human operators, and their mismanagement is
a leading contributor to process-safety incidents. Full autonomy in other
domains usually leans on a safe stop. A chemical plant does not have that
recourse because stopping is itself a hazardous and expensive operation.

This project asks whether a general-purpose large reasoning model (LRM), with
no task-specific training and only the information available to an operator,
can manage abnormal situations at run time, provided it acts through an
interface that cannot express an unsafe command.

{{< figure src="/projects/lrm-asm-architecture.png" align="center" alt="A large reasoning model sits in an abnormal-situation-management layer above a regulatory control layer, connected through a programmatic validator and a digital-twin forward simulation." caption="The LRM operates as an abnormal-situation-management layer above the decentralized regulatory (PID) controllers. It sees only a measured process-state summary and proposes actions from a bounded interface, and every proposal passes a programmatic validator backed by a digital-twin shadow rollout." >}}

**How it is guarded**

- **Bounded action interface.** The model chooses among a small set of generic
  supervisory moves. It can adjust setpoints, reconfigure control, run a
  procedure, distrust a suspect instrument, do nothing, or recommend shutdown.
  Direct actuator manipulation is not representable.
- **Programmatic validator.** Every proposal is checked against static bounds,
  rates, cooldowns, and a per-episode budget. The validator returns
  machine-readable reasons for a single revision.
- **Shadow rollout.** A nominal-model digital twin serves two roles. The model
  queries it to reason about a candidate action, and the validator runs it as
  a shadow simulation to veto any move predicted to trip the plant.

Knowledge is split in two. A process-agnostic reasoning doctrine lives in the
system prompt, while a generated, plant-specific description supplies the
numbers and mechanisms. Moving to a new process means regenerating one
document rather than re-engineering the method.

The benchmark covers 39 episodes on a plant-wide industrial process built on
the Tennessee Eastman simulator. The episodes span cases where no intervention
is needed, cases where a safety limit is approached, and cases where a
commanded quality change exceeds what the baseline can track. The model kept
the plant within every hard constraint in every episode.

---

*Code and benchmark are available at* [github.com/khalidlabs/safetep-core](https://github.com/khalidlabs/safetep-core),
*built on the* [TEP Studio](/projects/tep-studio/) *simulation kernel.*
