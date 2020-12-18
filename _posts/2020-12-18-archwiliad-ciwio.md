---
layout     : post
title      : "Bias Archwilio mewn Systemau Ciwio"
language   : cymraeg
comments   : true
---

Pan bod bysiau trwy'r amser yn hwyr? Pam bod fy ffrindiau yn fwy poblogaidd na fi? Y paradocs archwilio. Yn ddiweddar recordiais ddarlithoedd fideo ar gyfer fy [nghwrs llythrennedd data](/prelim2/) semester nesaf, a thrafodais bach am y paradocs archwilio a bias archwilio. Mae ond yn ffenomenon bach, ond mae'n briodol i systemau ciwio, ac felly efallai bod deall e'n ddiddorol.

Rwy'n credu bod [y cofnod blog hon](https://towardsdatascience.com/the-inspection-paradox-is-everywhere-2ef1c2e9d709) gan Allen Downey yn ei esbonio orau - yn y llyfr Orange Is The New Black mae'r awdur yn mynd i'r carchar ac wedi synnu bod gan ran fwyaf o'r bobl mae hi'n cwrdd dedfrydau hir iawn, hirach na'r hyd ddedfryd cymedrig y mae'r barnwr yn eu rhoi. Beth sy'n mynd ymlaen? Bias archwilio. Mae menywod sydd efo dedfrydau byr yn treulio llai o amser yn y carchar, felly mae llai o siawns byddant yna pan rydych chi'n mynd i'r carchar. Mae menywod sydd efo dedfrydau hir yn treulio mwy o amser yn y carchar, felly mae mwy o siawns byddant yna pan rydych chi'n mynd i'r carchar.

System ciwio heb byffer yw carchar. Felly gall systemau ciwio profi bias archwilio. Wrth parametreiddio model ciwio, os nad oes set data llawn ar gael, efallai byddwn ond yn cymryd "cliplun" o'r system. Er enghraifft os hoffwn wybod dosraniad hyd ddedfrydau mewn carchar, gallwn fynd i'r carchar ar ryw set o ddiwrnodau a gofyn y carcharorion sydd yna pa mor hir yw eu dedfrydau. Mae gan y data hwn a chaglir bias archwilio, ac felly bydd angen ei drawsnewid yn ôl i'r dosraniad gwreiddiol cyn ei ddefnyddio i fodelu'r carchar fel system ciwio.

Ystyriwch dau hapnewidyn di-dor: $$X$$ yw hyd y ddedfryd, gyda ffdt $$f(x)$$; ac $$Y$$ yw'r hyd ddedfryd _a arsylwir_ yn y cipluniau hyn, gyda ffdt $$g(x)$$. Beth yw'r perthynas rhwng $$X$$ ac $$Y$$?

Os yw hyd ddedfryd Agatha dwywaith hyd ddedfryd Barbara, yna byddwn yn disgwyl i'r tebygolrwydd o arsylwi Agatha i fod dwywaith y tebygolrwydd o arsylwi Barbara. Felly mae i'w weld bod y tebygolrwydd o arsylwi rhyw werth yn gyfrannol i'r gwerth ei hun, yn ogystal â'r wir debygolrwydd o'r gwerth hwnnw digwydd. Felly mae $$x f(x)$$ yn ddyfaliad da ar gyfer $$g(x)$$. Er mwyn gwneud hwn yn ffdt go iawn, bydd angen normaleiddio hwn, felly rhannwn gyda $$\int x f(x)$$, sydd digwydd bod gwerth disgwyliedig $$X$$. Felly gallwn ddyfalu bod:

$$g(x) = \frac{x f(x)}{\mathbb{E}[X]}$$

Gwiriwn ni hwn yn empirig gyda [Ciw](https://ciw.readthedocs.io/cy/latest/). Dywedwn fod $$X \sim \text{Unffurf}(3, 11)$$, dewiswn ddosraniad dyfodi mympwyol a chynhwysedd anfeidraidd:

{% highlight python %}
>>> import ciw
>>> N = ciw.create_network(
...     arrival_distributions=[ciw.dists.Exponential(10)],
...     service_distributions=[ciw.dists.Uniform(3, 11)],
...     number_of_servers=[float('inf')]
... )
{% endhighlight %}

Efelychwn y system am 500 uned amser i ddechrau er mwyn twymo'r system, yna cymerwn 'gipluniau' ar gyfnodau rheolaidd a recordiwn ni'r hydoedd dedfryd  y carcharorion sy'n bresennol ar yr amseroedd hynny:

{% highlight python %}
>>> amseroedd_archwilio = [500 + (i * 20) for i in range(100)]
>>> amseroedd = []
>>> for t in amseroedd_archwilio:
...     Q.simulate_until_max_time(t)
...     amseroedd += [ind.service_time for ind in Q.nodes[1].all_individuals]
{% endhighlight %}

Nawr cymharwn ni'r dosraniadau damcaniaethol $$f(x)$$ ac $$g(x)$$, i'r dosraniad empirig `amseroedd` y cawsom ni o'r cod uchod:

![]({{site.baseurl}}/images/uniform-cy.png)

Gwelwn fod y bias archwilio wedi digwydd fan hyn, a bod ein dosraniad damcaniaethol $$g(x)$$ yn ffitio'r dosraniad empirig yn dda.
Gwiriwn ni hwn eto gyda chwpl o ddosraniadau gwahanol.

+ Dosraniad trionglog gyda sgiw positif, $$X \sim \text{Trionglog}(4, 5, 14)$$:

![]({{site.baseurl}}/images/triang-pos-cy.png)

+ Dosraniad trionglog gyda sgiw negatif, $$X \sim \text{Trionglog}(2, 13.5, 16)$$:


![]({{site.baseurl}}/images/triang-neg-cy.png)

+ Dosraniad esbonyddol, $$X \sim \text{Esbonyddol}(2)$$:

![]({{site.baseurl}}/images/expon-cy.png)

Mae hwn eithaf neis. Mae hefyd yn gweithio ar gyfer ciwiau gyda nifer feidraidd o weinyddion a byffer, sydd ond yn oedi'r arsylwadau (ond dydw i ddim yn credu bydd hwn yn gweithio ar gyfer ciwiau blaenoriaeth).
Efallai bod ein dyfaliad o'r perthynas rhwng $$g(x)$$ ac $$f(x)$$ yn wir.
Os ydy, o ddosraniad empirig o $$g(x)$$ wedi cymryd o gipluniau o'r system, gallwn ei thrawsffurfio yn ôl i $$f(x)$$ i'w ddefnyddio yn ein modelau:

$$f(x) = \frac{\mathbb{E}[X] g(x)}{x}$$

Wrth gwrs dydyn ni ddim yn gwybod beth yw $$\mathbb{E}[X]$$ eto, ond does dim ots, mae ond yna i'w normaleiddio er mwyn iddo fod yn ffdt go iawn.

Yn Python:

{% highlight python %}
>>> import matplotlib.pyplot as plt
>>> empirig = plt.hist(amseroedd)
>>> amleddau = empirig[0]
>>> canolbwyntiau = [(i + j) / 2 for i, j in zip(empirig[1][:-1], empirig[1][1:])]
>>> trawsffurf = [p / x for x, p in zip(canolbwyntiau, amleddau)]
{% endhighlight %}


![]({{site.baseurl}}/images/inspection-transform-back-cy.png)

