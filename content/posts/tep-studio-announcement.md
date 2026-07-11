---
title: "TEP Studio: A New Implementation of the Tennessee Eastman Challenge"
date: 2026-05-27T00:00:00Z
draft: false
description: "A self-contained, fast, agent-accessible implementation of the Tennessee Eastman process, built for ML and reasoning systems."
tags: ["Projects", "Simulation", "Machine Learning", "Process Control"]
categories: ["Projects"]
---

TEP Studio is a new implementation of the Tennessee Eastman challenge problem.

The Tennessee Eastman process has been a standard testbed for process control and
fault diagnosis for three decades because it models a real industrial plant, with
its full nonlinearity, coupling, and disturbance structure. TEP Studio brings
that model into a form that ML and reasoning systems can use directly.

Three properties distinguish it:

1. It is a self-contained Python implementation, and it is able to simulate one
   process-hour in 8 ms — more than five times faster than the Fortran reference
   and about two orders of magnitude faster than an existing Python
   implementation.
2. It allows for systematic LLM access. The process description is exposed
   through a Model Context Protocol (MCP) server.
3. It is built from the bottom up to serve ML and data-intensive applications. It
   is also a Gymnasium environment, so reinforcement learning and control methods
   can train on it directly.

Code is on [GitHub](https://github.com/khalidlabs/tep-studio), and you can try the
simulator live in the [TEP Studio demo](/tep/). I've also written up the design
principles behind it in more detail on the [projects page](/projects/tep-studio/).
