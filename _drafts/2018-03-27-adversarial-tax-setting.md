---
layout: post
title: Tax optimisation as an adversarial game
---

I came across a new adversarial setting (at least new to me...) while getting curious about how to apply AI/ML to complete tax law and how to regulate tax optimisation (aka avoidance in my mind, sigh).

Some background:

> NZ uses a General Anti-Avoidance Rule (GAAR). In practice this means judiciaries end up making the law. Aka, there doesnt exist a set of well-specified laws, so judges must interpret the GAAR (expensive calls to the oracle). The rulings are then used as precedent for the future.

Ok, so this post focuses on two ideas.

<side>but if we could classify all types of avoidance then tax law would be complete??? kinda? ...</side>

- Completing tax law. (a formal set of rules)
- <a href="#classifying-tax-avoidance">Classifying avoidance</a>. (precedent and judges interpretation)

## Completing tax law

Current tax law is incomplete, we have an incomplete approximation of some ideal, complete body of tax laws. We use queries to judiciaries to complete the law.

### An adversary

Imagine a game between [IRD](https://www.ird.govt.nz/) and a taxpayer (from the perspective of IRD)  



<side>Huh, a property of the minima (wrt to IRDs actions) would be that dLoss/dAdversary would also = 0. It doesnt matter what the adversary does, our loss remains the same, tax cant be avoided (although maybe they could pay more than necessary). Is that because it is a zero-sum game?</side>

1. You reveal your move (write and pass some tax legislation).
2. Your adversary (a taxpayer) organises its finances to minimise tax paid (legally or not, that is a question for another day. Tomorrow).
3. The loss is revealed to the adversary (they avoided $x$ dollars of tax). You recieve the aggregated loss over all taxpayers (you can choose to query an expensive oracle -- judges/court -- to check whether your adversary has made a legal move).


What makes this setting hard?
- __Information asymmetry__. The adversary always gets access to the current loss (they know how much tax they avoided -- at least with respect to their moves). While you only get access to the aggregated loss. But you can get info about specific taxpayers if you query an expensive oracle (audits/jidiciaries).
- __Computation asymmetry__. The adversary needs to find a single strategy to minimise tax (that is also legal). You need to find and subvert all potential strategies to avoid paying tax.
- __Memory asymmetry__. In the multiplayer setting (many adversaries), it is easy(er) for each adversary to model and track changes in tax law (maybe they even collaborate...). But it is hard(er) for you to model and track changes to thousands, or more, adversaries (changes in a corporations finances my be indicative of avoidance).

### Related: Adversarial examples

Adversarial examples are typically framed as black box problems (at least as far as I have seen), but what if you know that your adversary is going to be given your current model? How would you design your model given that information? Design a model so that it is stable under an informed adversarial attack.

There is a target function (implicitly known by judges and the high court), which captures tax avoidance. We are trying to approximate that implicit knowledge with few samples. But, as we learn our approximation (the law -- no? and yes!?), our adversaries (taxpayers) adapt their strategies. So, while learning to approximate the target function we want to minimise taxpayers ability to game our approximation.

## Classifying tax avoidance

Tax avoidance is defined as (in my own words); when a law is used in a way that was not intended.

<!-- set of actions that are legal, but when viewed from a 'global' perspective, their only purpose is to avoid tax. -->

The more formal version is:

### Credit assignment

So if we have a set of loss function that capture the tax payers goals, ... and tax minimisation.

Can we assign credit to certain actions? WANT: this (set of) action(s) minimised tax paid, and did little else. (in fact, it made the company have a more complex structure and harder to run everyday.)

## Related work

<side>TODO Need to investigate other work using these asymmetries. Also what examples are there of problems that share these asymmetries?</side>
Aside from the asymmetries, this setting is similar to;

(Do any connections to mechanism design come to mind? I imagine there must be some previous work on this question.)
Learning a loss function. Which GANs are a good example of.
The key here us that we (the loss learner) have some finite capacity to check whether agents are exploiting our incomplete loss fn. How do you choose to spend your resources?


What would it look like if GANs shared these asymmetries?
```python
for _ in range(iterations):
    # player one makes its move
    discriminator = discriminator.update(loss)
    discrim = discriminator.freeze()

    # player two recieves the discriminator and
    # uses it to search for a low loss strategy
    generator = generator.train(discrim, iters=N)

    # the change in loss from generator at
    # step=0 to step=N is the loss
    loss = generator.loss(t=N) - generator.loss(t=0)
    dparams = generator.params(t=N) - generator.params(t=0)

    # maybe check the legality of the generators move
    # the loss is only revealed to the discriminator if
    # the oracle is queried. returns None if is not checked
    loss = maybe_check(loss, dparams)  
```

TODO. Relationship to reinforcement learning and reward hacking? And some of the safety research?
https://worldmodels.github.io/
Overfitting to approximate models, can do well in the virtual world, but poorly in the real world.

```python
# build an approximate model of the true dynamics
# aka construct some tax law to match intuition about right/wrong
for _ in range(iterations):

    o = env.step(a)

    # fit your model of tax law to observations
    # might not get these very often
    h = V(o)
    z_ = M(h, z)
    o_ = V_(z_)
    loss = d(o, o_)

# use the virtual/approximate model to
# learn a policy given some reward fn.
for _ in range(iterations):
  o = M.step(a)

  h = V(o)
  z_ = M(h, z)

  a = C(z_)
  r = R(z_)  
  # this issue is avoided in the paper.
  # how do we know R in the virtual environment?!?
```

We have a model. The set of laws.
And a loss function. How much the laws are gamed (aka unexpected use of the model?). Under the model, is a set of actions avoidance?


***
Questions raised;

* How can we design an un-gameable model, or what might be called a complete set of laws?
* How much harder is it to design un-gameable systems than to game that system?
* How would you even prove that a strategy is un-gameable?
* Is there a measure of gameability? The ability to __easily__ find hacks/strategies?
<side>What about retrospective application of the law? Need to investigate</side>



Legal questions

* What if I am overpaying my tax and then reorganise my finances so that I now pay as much as I 'should' be.
* The law seems to be two things? Specifies (some of) the allowable moves, a classifier of avoidance.
