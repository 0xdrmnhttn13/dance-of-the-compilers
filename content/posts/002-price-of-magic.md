---
title: "The Price of Magic"
date: 2026-08-19
description: "Working through T-gate injection by hand: what it really means to consume a magic state."
---

In the previous note, I learned why magic states have to exist.

The Clifford group is honest, but honesty alone cannot reach universality. So Clifford is not enough. How do we go beyond the Clifford group?

We need an operation that is not Clifford. A common choice is the $T$ gate:

$$
T =
\begin{pmatrix}
1 & 0 \\
0 & e^{i\pi/4}
\end{pmatrix}.
$$

Now we have

$$
\{\text{Clifford}, T\}.
$$

This gate set is universal.

That means the $T$ gate gives us something the Clifford group alone cannot provide.

But it also creates a problem.

The operation that gives us universality is exactly the kind of operation that does not preserve the Pauli structure in the same convenient way.

For example,

$$
TXT^\dagger
= \frac{X+Y}{\sqrt{2}}.
$$

Instead of mapping one Pauli operator into another Pauli operator, the $T$ gate takes us outside that simple structure.

So we arrive at an uncomfortable situation:

$$
\boxed{
\text{the operations that are easy to protect}
\neq
\text{the operations we need for universal computation}
}
$$

How do we cross that gap?

## Instead of applying $T$, store $T$ inside a state

Let us say we can prepare

$$
|A\rangle = T|+\rangle.
$$

Since

$$
|+\rangle
= \frac{|0\rangle+|1\rangle}{\sqrt{2}},
$$

we get

$$
|A\rangle
= \frac{|0\rangle+e^{i\pi/4}|1\rangle}{\sqrt{2}}.
$$

The non-Clifford phase

$$
e^{i\pi/4}
$$

is already present inside the state.

We can consume this state through measurement to obtain the effect of $T|\psi\rangle$.

By the concept this is magic-state injection.


$$
\text{hard operation}
$$

becomes

$$
\text{special resource state}
+
\text{protected operations}.
$$

We do not remove the difficulty. We just move the difficulty into state preparation. The $T$ gate is no longer the main character of the operation we need to execute. It becomes a resource we need to prepare.

## What does it actually mean to consume this resource?

Let the data qubit be

$$
|\psi\rangle
= \alpha|0\rangle+\beta|1\rangle.
$$

Our target is

$$
T|\psi\rangle.
$$

Applying $T$ directly gives

$$
T|\psi\rangle
= \alpha|0\rangle + e^{i\pi/4}\beta|1\rangle.
$$

To make the notation simpler, define

$$
\omega=e^{i\pi/4}.
$$

Then

$$
T|\psi\rangle
= \alpha|0\rangle+\omega\beta|1\rangle
$$

and the magic state becomes

$$
|A\rangle
= \frac{|0\rangle+\omega|1\rangle}{\sqrt{2}}.
$$

The phase that we want in the final state, $\omega$, is already inside the magic state.

Now we need to transfer its effect into the computation.

## Consuming the resource

Combine the magic state with the data qubit (the qubit holding our algorithm):

$$
|A\rangle|\psi\rangle.
$$

Simply substituting both states gives

$$
\frac{1}{\sqrt{2}}
(|0\rangle+\omega|1\rangle)
(\alpha|0\rangle+\beta|1\rangle).
$$

Expanding it,

$$
\frac{1}{\sqrt{2}}
\left(
\alpha|00\rangle
+
\beta|01\rangle
+
\omega\alpha|10\rangle
+
\omega\beta|11\rangle
\right).
$$

The first qubit is the magic state, acting as control. The second qubit is the data, acting as target. We apply a CNOT gate, and the state becomes

$$
\frac{1}{\sqrt{2}}
\left(
\alpha|00\rangle
+
\beta|01\rangle
+
\omega\alpha|11\rangle
+
\omega\beta|10\rangle
\right).
$$

A simple regrouping gives

$$
\frac{1}{\sqrt{2}}
\left[
(\alpha|0\rangle+\omega\beta|1\rangle)|0\rangle
+
(\beta|0\rangle+\omega\alpha|1\rangle)|1\rangle
\right].
$$

Now we measure the second qubit. The first qubit becomes the output of the injection protocol.

There are two possible outcomes:

$$
m=0
$$

or

$$
m=1.
$$

## What happens when $m=0$?

If the measurement gives $m=0$, we collapse onto first branch.

The remaining state is

$$
\alpha|0\rangle+\omega\beta|1\rangle.
$$

But this is exactly

$$
T|\psi\rangle.
$$

Therefore,

$$
\boxed{
m=0
\Rightarrow
T|\psi\rangle
}
$$

We never applied $T$ directly to the data qubit.

The phase was already stored inside $|A\rangle$.

The interaction and measurement transferred its effect into the output.

This is what makes the word **resource** start to feel concrete.

But quantum measurement is probabilistic.

We cannot expect to obtain $m=0$ every time.

So what happens when $m=1$?

## What happens when $m=1$?

If the measurement gives $m=1$, the remaining state is

$$
\beta|0\rangle+\omega\alpha|1\rangle.
$$

This is not yet $T|\psi\rangle$.

But now something important has happened.

The value $m=1$ is classical information.

We know which branch of the computation occurred.

That means we can correct it.

First apply the $X$ gate:

$$
X
\left(
\beta|0\rangle+\omega\alpha|1\rangle
\right).
$$

Since

$$
X|0\rangle=|1\rangle
$$

and

$$
X|1\rangle=|0\rangle,
$$

we obtain

$$
\omega\alpha|0\rangle+\beta|1\rangle.
$$

Now apply

$$
S=
\begin{pmatrix}
1 & 0 \\
0 & i
\end{pmatrix}.
$$

This gives

$$
\omega\alpha|0\rangle+i\beta|1\rangle.
$$

But $\omega=e^{i\pi/4}$, so

$$
\omega^2=e^{i\pi/2}=i.
$$

Therefore,

$$
\omega\alpha|0\rangle+i\beta|1\rangle
= \omega\alpha|0\rangle+\omega^2\beta|1\rangle.
$$

Factor out $\omega$:

$$
\omega
\left(
\alpha|0\rangle+\omega\beta|1\rangle
\right).
$$

The state inside the parentheses is exactly $T|\psi\rangle$.

So

$$
SX|\text{branch}_{m=1}\rangle
= \omega\, T|\psi\rangle.
$$

The extra factor $\omega$ is only a global phase.

Therefore, physically,

$$
\omega T|\psi\rangle
\sim
T|\psi\rangle.
$$

So both branches work:

$$
m=0
\Rightarrow
T|\psi\rangle,
$$

while

$$
m=1
\Rightarrow
SX
\Rightarrow
T|\psi\rangle
$$

up to a global phase.

Now we can see more clearly what injection actually does.

We are not constructing a non-Clifford gate from Clifford gates.

The non-Clifford part already exists inside the resource state.

The Clifford operations, measurement, and classical correction only allow us to consume that resource and transfer its effect into the computation.

So the process is

$$
\text{prepare }|A\rangle
\;\to\;
\text{Clifford interaction}
\;\to\;
\text{measurement}
\;\to\;
\text{classical correction}
\;\to\;
T|\psi\rangle.
$$

What happens if the state preparation is imperfect?
Then the magic carries its imperfections with it.

Injection tells us how to spend a magic state. It does not tell us how to produce one that is clean enough to trust.

And perhaps that is the real price of magic: the difficult operation did not disappear. We turned it into a resource, and now that resource has to be manufactured.

The machinery for doing that is called magic-state distillation.

I do not understand it well enough yet.

So that is the next thing I want to derive.
