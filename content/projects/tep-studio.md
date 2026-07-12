---
title: "TEP Studio and Self-Describing Process Simulators"
date: 2026-05-20T00:00:00Z
draft: false
description: "A simulator should publish one machine-readable process description from which every interface is derived. TEP Studio applies this principle in a fast Tennessee Eastman reference implementation."
tags: ["Simulation", "Reinforcement Learning", "MCP", "Process Control"]
categories: ["Projects"]
---

Dynamic process models are increasingly consumed by automated agents rather
than by control engineers reading source code. These agents include data
pipelines that assemble training sets, reinforcement-learning algorithms, and
language models. Each depends on process meaning that a numerical interface
does not expose, such as what each variable represents, which signals are
available online, and which limits trigger a shutdown. Today that meaning
lives in source code and informal convention, so recovering it is error-prone
and does not transfer across a model's many independent implementations.

The design principle is that a simulator should be self-describing. It
publishes one machine-readable process description, and that description is
the single source from which every interface is derived.

{{< figure src="/projects/tep-studio-architecture.png" align="center" alt="A single machine-readable process description sits above the process-model core and below four interfaces for online interaction, trajectory data, estimation and optimization, and agent access, each serving people, algorithms, or reasoning models." caption="One description, many views. The transition core advances the process. The online-interaction, trajectory-data, estimation and optimization, and agent (MCP) interfaces are all derived from the same description, so engineers, algorithms, and reasoning models act on one definition of the process." >}}

**Reference implementation**

TEP Studio applies the principle to a modified Tennessee Eastman process, a
standard testbed for three decades because it captures a real plant's
nonlinearity, coupling, and disturbance structure.

- **Fast.** A self-contained Python implementation simulates one process-hour
  in about 8 ms. That is more than five times faster than the Fortran
  reference and about two orders of magnitude faster than an existing Python
  implementation.
- **RL-ready.** It is a Gymnasium environment, so reinforcement-learning and
  control methods can train on it directly.
- **Agent-accessible.** The process description is exposed through a Model
  Context Protocol (MCP) server, giving language models structured access to
  the same semantics.

The interfaces for online control, trajectory data, estimation and
optimization, and agent access are all generated from the same description,
so a single definition is shared instead of restated for each consumer.

---

*The code is at* [github.com/khalidlabs/tep-studio](https://github.com/khalidlabs/tep-studio),
*and a live simulator runs at* [khalidlabs.com/tep](/tep/).
