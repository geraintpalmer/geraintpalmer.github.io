---
layout     : post
title      : "The Borsuk-Ulam Theorem"
language   : english
comments   : true
---

Today I learned something I thought was awesome.
My colleague
[Dr. Timm Oertel](https://www.cardiff.ac.uk/people/view/192658-oertel-timm)
introduced me to this nice little theorem: the Borsuk-Ulam theorem.
It roughly says: *Every continuous function on an n-sphere to Euclidean n-space
has a pair of antipodal points with the same value*.

What does this mean?

# Circles

**For a continuous function on a circle, there exists a pair of opposite points
on the circle with the same value.**

Imagine a 2D world covered in continuous mountains (no vertical cliffs or
drops):

<img src="{{site.baseurl}}/images/globe.png" width="350">{: .center-image }

This theorem tells us that there exists a pair of points exactly opposite each
other, with the exact same mountain height:

<img src="{{site.baseurl}}/images/globe_antipodal.png" width="350">{: .center-image }

Why is this true?
Well we can flatten out this world as a one dimentional function $$f(x)$$,
comparing the top of the circle (positive $$x$$) to the bottom (negative $$x$$):

<img src="{{site.baseurl}}/images/flattened.png" width="750">{: .center-image }

+ A pair of opposite points on the circle would be the negative of the other,
$$y$$ and $$-y$$.
+ If they both have the same value or height, then $$f(y) - f(-y) = 0$$.
+ Consider the function $$g(x) = f(x) - f(-x)$$.
+ This is an odd function, as
$$g(-x) = f(-x) - f(x) = -\left(f(x) - f(-x)\right) = -g(x)$$:

<img src="{{site.baseurl}}/images/flattened_diff.png" width="750">{: .center-image }

A continuous odd function always has a zero (it is continuous so no jumps, and
must pass from $$-g(x)$$ to $$g(x)$$).
So there must exist some value $$y$$ such that
$$g(y) = f(y) - f(-y) = 0$$, that is opposite points that have the same height.


# Spheres

In more diementions this is even more bonkers!
The full statement of the theorem gives that for continuous function
$$f: S^n \rightarrow \mathbb{R}^n$$ there exists a point $$y$$ such that
$$f(y) = f(-y)$$.

On a sphere, $$f$$ is a function with two values.
For example, consider the Earth as a sphere, and $$f$$ is a function that gives
the values of the temperature and humidity (reasonably assuming that both
are continuous).
There exists two points exactly opposite eachother on the Earth that have the
exact same temperature and humidity!

This is also dicussed in this [Forbes article](https://www.forbes.com/sites/kevinknudson/2016/05/28/how-topology-affects-the-weather/#775f680535a5).
Considering any higher dimentions would hurt my brain, but these examples blew
my mind.