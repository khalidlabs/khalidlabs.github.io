---
title: "TEP Studio: Self-Describing Process Simulators"
date: 2026-05-15T00:00:00Z
draft: false
description: "A design principle — a simulator should publish one machine-readable process description that every interface is derived from — with a fast Tennessee Eastman reference implementation for people, algorithms, and reasoning models alike."
tags: ["Simulation", "Reinforcement Learning", "MCP", "Process Control"]
categories: ["Projects"]
---

Dynamic process models are increasingly consumed by automated agents rather than
by control engineers reading source code: data pipelines that assemble training
sets, reinforcement-learning algorithms, and language models. Each of them
depends on *process meaning* that a numerical interface does not expose — what
each variable represents, which signals are available online, and which limits
trigger a shutdown. Today that meaning lives only in source code and informal
convention, so recovering it is error-prone and does not transfer across a
model's many independent implementations.

The design principle here is that a simulator should be **self-describing**: it
publishes one machine-readable process description **S** that is the
single source from which every interface is derived.

{{< figure src="/projects/tep-studio-architecture.png" align="center" alt="A single machine-readable process description sits above the process-model core and below four interfaces — online interaction, trajectory data, estimation and optimization, and an agent interface — each serving people, algorithms, or reasoning models." caption="One description, many views. The transition core advances the process; the online-interaction, trajectory-data, estimation/optimization, and agent (MCP) interfaces are all derived from the same description, so engineers, algorithms, and reasoning models act on one definition of the process." >}}

**Reference implementation**

TEP Studio applies the principle to a modified Tennessee Eastman process — a
standard testbed for three decades because it captures a real plant's
nonlinearity, coupling, and disturbance structure.

- **Fast.** A self-contained Python implementation simulates one process-hour in
  about 8 ms — over five times faster than the Fortran reference and roughly two
  orders of magnitude faster than an existing Python implementation.
- **RL-ready.** It is a Gymnasium environment, so reinforcement-learning and
  control methods can train on it directly.
- **Agent-accessible.** The process description is exposed through a Model
  Context Protocol (MCP) server, giving language models structured access to the
  same semantics.

The interfaces for online control, trajectory data, estimation and optimization,
and agent access are generated from **S** rather than restated per
consumer — so a single definition is shared instead of drifting apart across
tools.

---

*Code:* [github.com/khalidlabs/tep-studio](https://github.com/khalidlabs/tep-studio) ·
*Try it live:* [TEP Studio simulator](/tep/)
