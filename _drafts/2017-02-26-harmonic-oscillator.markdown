---
title: "Optimization and sampling methods Part 2: The harmonic oscillator"
layout: post
comments: true
date: 2017-02-26 14:50
headerImage: false
published: true
tag:
- physics
- optimization
- maths
- molecular dynamics
- monte carlo
- machine learning
- gradient descent
description: This is part 2 in a short series of posts about methods for finding local minina, and on using molecular dynamics or Monte Carlo methods to sample from functions. Here I introduce the harmonic oscillator, an important physical model, and relate it to what we did in part 1.
---

## The harmonic oscillator

In [part 1]({{ site.baseurl }}{% link _posts/2017-02-08-Optimization-and-sampling-methods-part-1.markdown %})
we introduced gradient descent and used it to optimize a simple 1-d equation,

$$ y(x) = x^2. $$

While this is a pretty simple problem, it actually describes an incredibly
important physical model: the **harmonic oscillator** (i.e. a spring).
It's immportant because it's one of the few problems in physics we can 
actually solve exactly, and it turns out that even anharmonic functions 
are approximately harmonic near their minimum.

The potential energy of a harmonic oscillator with spring-constant 
\\(k\\) is \\(V(x) = \frac{1}{2}k x^2\\),
and the force on it is \\(F(x) = -\frac{dV}{dx} = -k x\\) (Hook's Law). 
Note the similarities with **gradient descent**, it turns out we actually 
found the minimum of a harmonic oscillator with \\(k=2\\), and the 
derivative (slope) in gradient descent corresponds to the force!
To be consistent with the previous part we'll work with \\(k=2\\) for the 
rest of this article.

## Molecular dynamics

Since we are now considering a physical system we can do more than just find 
the minimum state: we can see how it evolves with time. To do this, we need 
just a little bit more physics: **the principle of conservation of total energy**.
This means that when the harmonic oscillator moves to a state with lower 
potential energy \\(V\\), it gains some **kinetic energy** \\(T\\) equal to 
the amount of potential energy it lost. If \\(E\\) is the total energy then 
we can write this as,

$$ E = T + V. $$

Note that \\(T\\) in the above equation is not really the temperature, and I 
say not *really* because on some level kinetic energy is very closely related 
to temperature, but that's beyond the scope of this article.

We'll introduce one more thing from physics: **time**. In the previous article 
\\(x\\) was the free parameter, but here \\(x(t)\\) will be the position of our 
oscillator at time \\(t\\).

## Euler method

Let's say we know at some time \\(t\\) we know the position of our spring
and so by the above equations we know its potential energy and the force 
acting on it.  If we wanted to know the position at some future time
\\(t + \Delta t\\), we can first to a Taylor expansion,

$$ x(t+\Delta t) = x(t) + \Delta t \frac{dx}{dt}(t) + \frac{1}{2}(\Delta t)^2 \frac{d^2x}{dt^2}(t) + O(\Delta t^3). $$

Since \\( \frac{dx}{dt}(t) \\) and \\( \frac{d^2x}{dt^2}(t) \\) are the velocity 
(\\(v(t)\\) and acceleration (\\(a(t)\\) respectively,
and \\( a(t) = F(t)/m \\) (where \\(m\\) is the mass), we can write,

$$ x(t+\Delta t) = x(t) + \Delta t v(t) + \frac{1}{2}(\Delta t)^2 \frac{F}{m}(t)  $$



