---
layout     : post
title      : "Atgof i'm Hun Nad yw \\(e\\) Mor Arbennig â Ni"
language   : cymraeg
comments   : true
---

Mae'r rhif $$e$$, rhif Euler, 2.7182818284..., *yn* arbennig.
Mae'n arbennig oherwydd fod::

$$\frac{d}{dx} e^x = e^x$$

Ond dyna un o'r *unig* rhesymmau y mae'n arbennig.

Mae i'w weld i gropian i fyny trwy'r amser, [twf poblogaethau](https://en.wikipedia.org/wiki/Population_model#Equations), [dadfeiliad ymbelydrol](https://en.wikipedia.org/wiki/Radioactive_decay#Mathematics_of_radioactive_decay), [hap-ddigwyddiadau](https://en.wikipedia.org/wiki/Poisson_distribution) ac [adlog di-dor](https://en.wikipedia.org/wiki/Compound_interest#Continuous_compounding).
Mae angen i atgoffa fy hun yn aml nad yw $$e$$ fel $$\pi$$ neu'r cymhareb euraidd $$\phi$$, dyw e ddim just *ddigwydd** gropian i fyny yn natur.
Mae yna oherwydd rydyn ni'n ei roi yna, defnyddiwn $$e$$ mewn modelau mathemategol gan ei fod yn hawdd i'w drin.

Ystyriwch model syml o twf poblogaeth:

$$N(t) = N_0 e^{ax}$$

Pam yw $$e$$ yna?
Na fyddant yn gwneud mwy o synwyr i defnyddio rhywbeth del $$2^x$$, yn golygu fod y poblogaeth yn dwblu pob uned amser?
Neu rhyw bôn arall i gwell adlewyrchu ymddygiad y poblogaeth?

Wel ewn gwirionedd maent yn **gyfatebol**.
Gallwn ysgrifennu unrhyw ffwythiant $$a^x$$ fel $$e^{bx}$$ ar gyfer rhyw dewis o $$b$$:

$$
\begin{align}
a^x &= e^{bx}\\
\log_a \left(a^x\right) &= \log_a \left(e^{bx}\right)\\
x &= bx \log_a \left(e\right)\\
1 &= b \log_a \left(e\right)\\
\frac{1}{\log_a \left(e\right)} &= b
\end{align}
$$

Felly:

$$a^x = e^{\frac{1}{\log_a(e)}x}$$

Trwy cymhwyso $$\log_e$$ neu $$\ln$$ i'r ddwy ochr cawn fformiwla newid bôn ar gyfer logiau:

$$\log_c(y) = \frac{\log_d(y)}{\log_d(c)}$$