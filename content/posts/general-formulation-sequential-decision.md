---
title: "An Opinion on the General Formulation of Sequential Decision Problems"
date: 2026-06-24T00:00:00Z
draft: false
description: "Why the reduced problem a field actually studies — not the maximal formulation — is usually the one that matters in practice."
tags: ["Reflections", "Control Systems", "Reinforcement Learning", "Optimization"]
categories: ["Reflections"]
---

I came to control and reinforcement learning from chemical engineering, and in
that passage the general formulation of the sequential decision problem was
valuable to me, as a means of reading across fields in which I held no native
vocabulary (thanks to legends like Dimitri Bertsekas and Warren Powell).
However, for most researchers and practitioners, the object of interest is not
the general formulation but the reduced problem that a particular field actually
studies.

The most general formulation presents a policy that minimizes the expected
cumulative cost over a horizon, where the state consists of a physical component,
the deterministic information available at the moment of decision, and a belief
over the quantities that remain unknown. Warren Powell sets out such a maximal
formulation. But what does this generality imply for practice?

The formulation is maximal in the sense that it admits, at the same time, every
principal source of difficulty. There is a state that evolves under control,
there is exogenous information revealed over time, and there is uncertainty in
the model itself. Even though there are problems of interest that possess all
three at once, one does not, however, work within the general formulation. In a
given field one adopts the assumptions that are standard there, and those
assumptions remove or approximate one or more of the terms above. What remains
is, in nearly every case, the formulation with which the field already begins.

Model predictive control provides a clean illustration. Suppose the model is
taken as known and the uncertain future is replaced by a nominal forecast. The
belief state then vanishes, the expectation over the exogenous process collapses,
and one is left with a deterministic optimization over a finite horizon, resolved
again at each stage. This is the standard model predictive control problem, and
it is the point of departure for the control engineer, who reaches it without
ever traversing the general form. Other fields suppress other terms and arrive at
their own points of departure.

I believe that the reduced problem is the one that matters. In adopting the
assumptions and the formulation standard in a field, one inherits the theoretical
apparatus that field has developed upon them, including its stability and
convergence results, its duality theory, and its estimators. The general
formulation, whatever its reach, supplies none of this. The general formulation
is an important contribution that highlights some common threads among disparate
fields, but I cannot see how or why the status quo would change.
