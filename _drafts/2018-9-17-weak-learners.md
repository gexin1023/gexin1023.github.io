---
layout: post
title: Ensembles of weak learners
---

Have an ensemble of weak learners when composed together can make a strong learner.

Markets. You have private information and use it to make bets about future prices.
Together, all the participants in the market integrate their information so that the price refects the true value.

Problem: because bets interact additively information can only be additive.
yet i might have a peice of info that non-linearly effects the price? thus this info cannot be integrated into the market.

surely a market that actually shared the private information would have more accurate estimates of the price? (but little infentive/maybe people will lie...?)

***

The price, $p$, on the market is determined by $f, g$'s etimate of the value of $x$, given private information.

$$
\begin{align}
p &= f(x, i_f) \circ g(x, i_g) \\
&\ne h(x, i_f, i_g) \\
\end{align}
$$

How do different valuations combine on the market? Additively? If so then $\circ = +$ and we have $f(x, i_f) + g(x, i_g)$. But I can easily imagine situations where knowing $i_f$ and $i_g$ could non-linearly alter my valuation.

So is the market really able to integrate the information!?

## Resources

#### Ensembles

- https://en.wikipedia.org/wiki/Boosting_(machine_learning)
- [The Strength of Weak Learnability](http://www.cs.princeton.edu/~schapire/papers/strengthofweak.pdf)
- [On the Equivalence of Weak Learnability and Linear Separability](http://colt2008.cs.helsinki.fi/papers/26-Shwartz.pdf)
- [AdaBoost](https://en.wikipedia.org/wiki/AdaBoost)
- [Ensemble methods](http://www2.islab.ntua.gr/attachments/article/86/Ensemble%20methods%20-%20Zhou.pdf)


#### Markets

- ?
