---
layout     : post
title      : "Reminder to Self That \\(e\\) Isn't That Special"
language   : english
comments   : true
---

The number $$e$$, Euler's number, 2.7182818284..., *is* special.
It's special because:

$$\frac{d}{dx} e^x = e^x$$

But that's one of the *only* reasons it's special.

It seems to pop up all the time, [population growth](https://en.wikipedia.org/wiki/Population_model#Equations), [radioactive decay](https://en.wikipedia.org/wiki/Radioactive_decay#Mathematics_of_radioactive_decay), [random events](https://en.wikipedia.org/wiki/Poisson_distribution) and [continuous compound interest](https://en.wikipedia.org/wiki/Compound_interest#Continuous_compounding).
I've found that I keep needing to remind myself that $$e$$ isn't like $$\pi$$ or or the golden ratio $$\phi$$, it doesn't just *happen* to pop up in nature.
It's there because we put it there, we use $$e$$ in mathamatical models because it's easy to manipulate.

Consider a simple population growth model:

$$N(t) = N_0 e^{ax}$$

Why is $$e$$ there?
Wouldn't it make more sense to use something like $$2^x$$, meaning the population doubles every time unit?
Or some other base to better reflect the behaviour of the population?

Well actually they are **equivalent**.
Any exponential function $$a^x$$ can be written as $$e^{bx}$$ for some choice of $$b$$:

$$
\begin{align}
a^x &= e^{bx}\\
\log_a \left(a^x\right) &= \log_a \left(e^{bx}\right)\\
x &= bx \log_a \left(e\right)\\
1 &= b \log_a \left(e\right)\\
\frac{1}{\log_a \left(e\right)} &= b
\end{align}
$$

So:

$$a^x = e^{\frac{1}{\log_a(e)}x}$$

Applying $$\log_e$$ or $$\ln$$ to both sides gives the change of base formula for logs:

$$\log_c(y) = \frac{\log_d(y)}{\log_d(c)}$$