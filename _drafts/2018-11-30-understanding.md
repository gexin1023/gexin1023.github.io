---
layout: post
title: Understanding
---

(explanation and understanding are used as synonyms, no not quite.)

## Explanation as generation

> “What I cannot create, I do not understand.”

> Mathematics is not about numbers, equtions, computation or algorithms, it is about understanding. William Paul Thurston

***
But, generation is neither necessary nor sufficient.

- Not necessary. We "understand" that we evloved from bacteria despite the fact that we cannot generate this phenomena. (maybe we dont really understand...)
- Not sufficient. A NN could just memorise its training data, but it does not understand its training data... (recovering a minimal representation, compression?)

There are different levels of explanation?

## Understanding as reachability

Understanding seems to involve a few ideas.

If you understand X, you can;
- explain it.
- use it flexibly to do Y.

Related to reachability and connectedness.

## Examples

We think we understand evolution, it works via natural selection (we can describe) $\delta s = f(s_t)$. But we cannot generate our observations. But. We can generalise from XX ...?

Despite the fact that (almost) no one could build a modern computer from scratch (even if provided the hardware, would have to write kernels, an OS, ...). Many of use think we understand how computers work.

(_more examples! things we do/dont understand. What is the distinction!?_)

## Limited capacity

__Q:__ How is it possible for a person (with limited resources, $X$) to understand a complex object or phenomena (which has complexity $Y$)? Consider the case when the resources available are far smaller than the complexity (when $X << Y$).

If you cannot generate it then how can we ever measure/falisfy our hypothesis? Independently verify modules, and make an inductive arguent.

Relies on an inductive argument.
Not possible to show that f(n) = y



***

Partial exlanations. What about explanations that are only partially accurate?
A measure of how well we understand something, U, could be: the cost and accuracy of generating X using our best explanation, E.

***

Goal is to generate X via a provided explanation.
e.g. Derive X from 'accepted/verifiable' assumptions, E.

Using a pogram specification, rules, objects, I can verify for my self that given E, X is a logical consequent (or is a likely consequent).

Understanding is a measure of;
(1) how much the explanation reduces the computational complexity of the derivation (the size of the search space).
(2) how accurately the explanation produces E.

If we are provided with the axioms of linear algebra we could prove that ???. But it would be computationally expensive. (how expensive!?) But if we were also provided with a proof that we could verify easily then ...

***

Imagine explaining how a computer calculates 2+2. We definitely dont go through a ll the details. The key is abstraction and generalisation. Understanding a simple model and how it might be scaled to the more complex thing we are trying to explain.

How does a compute calculate 2+2 vs 2103048824+47329823858124387?

Will need to be an inductive argument. f(n+1)... The ability to generalise over n. So despite the fact that we might not have the computational resources to compute f(N) we might understan how f(n) is related to f(n+1) and thus ...!?

## Induction

Refresher. Prove something famous via induction.

(statistical induction can be wrong... but forget about that for now)

***

Related

- necessary and sufficient causation


What makes something true?
- Spend X resources trying to find adversarial examples/counter examples (but not finding any)?!
- Ability to predict/generate accurately
- ?
