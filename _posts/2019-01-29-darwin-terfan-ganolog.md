---
layout     : post
title      : "Darwin, Lamarck, a'r Theorem Terfan Ganolog"
language   : cymraeg
comments   : true
---

Wythnos hon yw wythnos gyntaf nôl yn dysgu, ac rwy'n edrych ymlaen at ddysgu un o'm hoff fodiwlau Preliminary Mathematics II, lle rydym yn cyflwyno cysyniadau data a thebygolrwydd i fyfyrwyr tu allan i'r adran mathemateg.
Rydw i trwy'r amser yn cyflwyno'r dosraniad Normal trwy ddweud bod "nifer fawr o bethau naturiol yn dilyn y dosraniad Normal, er enghraifft taldra pobl". Dyma rywbeth rydw i wedi bod yn ailadrodd ers imi ei ddysgu yn yr ysgol. Ond pam yw hyn yn digwydd?

<img src="{{site.baseurl}}/images/NormalDist.png" width="350">{: .center-image }

Mae'n hawdd dechrau trwy siarad am [fwrdd Galton](https://en.wikipedia.org/wiki/Bean_machine) (neu beiriant ffa) sy'n dangos bod newidiadau bach cronnus naill ochr i ryw dechreubwynt yn achosi i'r safleoedd terfynol dilyn dosraniad Normal.

Fe allwn ddweud bydd taldra plentyn yn wahanol i daldra ei rhieni gan ryw newid bach, ac felly gallwn ddefnyddio'r bwrdd Galton hon yn esbonio pam bod taldra pobl yn dilyn dosraniad Normal.
Ond i fi roedd hwn yn ymddangos i fod yn esboniad eithaf gwan.

Gadewch i ni feddwl am theori Darwin o ddethol naturiol.


# Model Darwin

Gwyddon fod rhieni yn pasio priodweddau ymlaen i'w blant, fel arfer trwy gynhyrchu rhyw fath o "cymedr" o'r rhieni.
Credodd Darwin bod pob priodwedd a welwyd heddi (gan anwybyddu mwtaniadau) yn bodoli fel poblogaeth fawr yn y gorffennol, ac ond y cryfaf sy'n goroesi tan heddiw.
Hoffwn ddarganfod pam y mae beth sy'n goroesi tan heddiw yn dilyn dosraniad Normal.

Felly, efelychais boblogaeth amrywiol o 'daldra'.
Ar gyfer pob cenhedlaeth parais i rieni ar hap, ac maent yn cynhyrchu dau blentyn gyda'r priodweddau sydd yn gymedr taldra'u rhieni:

{% highlight python %}
>>> import random

>>> def next_gen_darwin(gen):
...     new_gen = []
...     random.shuffle(gen)
...     for i in range(len(gen)):
...         if i % 2 == 0:
...             g1 = (gen[i] + gen[i+1]) / 2
...             g2 = (gen[i] + gen[i+1]) / 2
...             new_gen.append(g1)
...             new_gen.append(g2)
...     return new_gen
{% endhighlight %}

Nawr dychmygwch fod gan y boblogaeth ddechreuol taldraoedd ar hap ac unffurf rhwng 2 ac 8 troedfedd.
Efelychu chwe chenhedlaeth:

{% highlight python %}
>>> random.seed(0)
>>> gens = [[random.uniform(2,8) for _ in range(500)]]
>>> for generation in range(6):
...     gens.append(next_gen_darwin(gens[-1]))
{% endhighlight %}

Wrth blotio'r dosraniad taldra pob cenhedlaeth gallwn weld ei fod yn agosáu at ddosraniad Normal:

<img src="{{site.baseurl}}/images/darwin-dists.png" width="350">{: .center-image }

Pam bod hwn yn digwydd? Cofiwch y Theorem Terfan Ganolog:

> Mae'r [Theorem Terfan Ganolog](https://en.wikipedia.org/wiki/Central_limit_theorem) yn dweud yn fras pan symiwyd samplau ar hap o $$n$$ hapnewidyn annibynnol, mae'r symiau hyn y dilyn dosraniad Normal wrth i $$n \to \infty$$.

Ystyriwch y $$k^{\text{fed}}$$ genhedlaeth:

+ Hwn yw dosraniad y symiau o samplau ar hap[^1] maint $$2$$ o'r genhedlaeth flaenorol (wedi rhannu â 2),
+ Yn ei dro hwn yw swm samplau ar hap maint $$2^k$$ o'r genhedlaeth gyntaf (wedi rhannu â $$2^k$$),

ac felly gallwn gymhwyso'r Theorem Terfan Ganolog: wrth i'r genhedlaeth $$k$$ cynyddu, bydd dosraniad y taldra yn agosáu at y dosraniad Normal (yn eithaf cloi), ac mae hyn yn esbonio'r ffenomenon bod taldra pobl yn dilyn dosraniad Normal.

"Ond arhoswch!" rydych yn gweiddi, "Y flwyddyn yw 1858 ac nid yw llyfr Origin of the Species Darwin wedi'i gyhoeddi eto!" A yw theori Lamarck hefyd yn ffitio?


# Model Lamarck

Cyn Charles Darwin, y brif theori oedd un Jean-Baptiste Lamarck.
Credodd Lamarck hefyd bod rhieni yn pasio'u priodweddau i'w blant. Ond yn lle credu bod pob amrywiaeth yn bodoli o'r dechrau, credodd bod rhywogaethau yn dechrau gyda phriodweddau homogenaidd, a bod unigolion yn gallu newid y priodweddau hynny dros gyfnod eu bywydau, ac maent yn pasio'r priodweddau newydd hyn i'w blant.

Felly, efelychais boblogaeth homogenaidd o 'daldra'.
Ar gyfer pob cenhedlaeth parais i rieni ar hap, maent yn newid ei briodwedd taldra (mae eu taldra yn cynyddu gan werth ar hap o ddosraniad unffurf rhwng $$-\epsilon$$ i $$\epsilon$$).
Yna maent yn cynhyrchu dau blentyn gyda thaldra sydd yn gymedr taldra newydd ei rhieni:

{% highlight python %}
>>> def next_gen_lamarck(gen, epsilon):
...     new_gen = []
...     random.shuffle(gen)
...     for i in range(len(gen)):
...         if i % 2 == 0:
...             parent1 = gen[i] + random.uniform(-epsilon, epsilon)
...             parent2 = gen[i+1] + random.uniform(-epsilon, epsilon)
...             g1 = ((parent1 + parent2) / 2)
...             g2 = ((parent1 + parent2) / 2)
...             new_gen.append(g1)
...             new_gen.append(g2)
...     return new_gen
{% endhighlight %}

Nawr dychmygwch fod gan ein poblogaeth taldra o 5 troedfedd yn union.
Efelychu chwe chenhedlaeth (gyda $$\epsilon = 0.7$$):

{% highlight python %}
>>> random.seed(0)
>>> gens = [[5.0 for _ in range(500)]]
>>> for generation in range(6):
...     gens.append(next_gen_lamarck(gens[-1], 0.7))
{% endhighlight %}

Wrth blotio'r dosraniad taldra pob cenhedlaeth gallwn weld ei fod yn agosáu at ddosraniad Normal unwith eto:

<img src="{{site.baseurl}}/images/lamarck-dists.png" width="350">{: .center-image }

Eto, ystyriwch y $$k^{\text{fed}}$$ genhedlaeth:

+ Hwn yw dosraniad y symiau o samplau ar hap maint $$2$$ o'r genhedlaeth flaenorol *ar ôl newid* (wedi rhannu â 2),
+ Y genhedlaeth flaenorol *ar ôl newid* yw swm yr elfennau o'r genhedlaeth flaenorol wreiddiol ac $$x \sim \text{Unffurf}(-\epsilon, \epsilon)$$,
+ Felly, yn ei dro, y $$k^{\text{fed}}$$ genhedlaeth yw swm y samplau ar hap maint $$2^k$$ o elfennau'r genhedlaeth gyntaf (cysonion o 5) adio $$kx$$ (ac wedi rhannu â $$2^k$$), lle $$x \sim \text{Unffurf}(-\epsilon, \epsilon)$$,

ac felly gallwn cymhwyso'r Theorem Terfan Ganolog unwaith eto, sy'n esbonio'r tuedd tuag at dosraniad Normal.


# Sylwadau

Dydy dadansoddiad y blog hwn ddim rili yn esbonio pam bod gan daldra pobl dosraniad Normal, oherwydd bod y modelau wedi'u gor-symleiddio.
Serch hynny, mae wedi rhoi dealltwriaeth mwy i mi o'r ffenomenon, ac felly bydd gennaf mwy o hyder yn siarad amdano yn y dosbarth.

---

[^1]: nid yw hwn ar hap go iawn, ond rydym ni yn paru rhieni ar hap felly...