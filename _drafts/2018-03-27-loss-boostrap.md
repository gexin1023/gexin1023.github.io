---
layout: post
title: Bootstrapping loss functions
---

> The evolutionary challenge of making unsupervised learning solve the “right” problems is, therefore, to find a sequence of cost functions that will deterministically build circuits and behaviors according to prescribed developmental stages, so that in the end a relatively small amount of information suffices to produce the right behavior. [source](https://www.frontiersin.org/articles/10.3389/fncom.2016.00094/full)

- Is it possible to bootsrap a loss function using itself?
- Have can we recursively learn a loss function?

We are given an incomplete loss function. Incomplete meaning;
- it doesnt fully capture the true loss
- it is inefficient?
- it is built out of many independent heuristics.
- ???

## Compression

If the loss measures compression then it would be possible to use the loss to measure itself? We could then search of better versions of itself.
In what cases would this work?

## Value fn

[Prefrontal cortex as a meta-reinforcement learning system](https://www.biorxiv.org/content/early/2018/04/06/295964)
using an existing, expensive, value fn to construct a more efficient/specialised value fn.

## Multiagent setting

Imagine we have n functions and a loss function. We pair the loss function with some of the n functions and proceed to optimise.
Imagine we have n functions and two loss functions. We pair the loss functions with any other functions, including other loss functions.
If loss functions share the same representation as the other functions then they could also be optimised.

Given n loss functions, each optimising others (and possibly themselves), what is their trajectory, how can we control it?

## ?

## Thoughts

* How is this related to;
  * self-replcating information,
  * composing symmetric objects to build more symmetric objects,
  * recursion
  * the inverse of meta learning
  *
