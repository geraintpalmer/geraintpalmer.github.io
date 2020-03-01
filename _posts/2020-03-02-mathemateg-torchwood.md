---
layout     : post
title      : "Torchwood: Mathemateg 'Miracle Day'"
language   : cymraeg
comments   : true
---

Rydw i wedi bod yn gwylio lot o [Torchwood](https://cy.wikipedia.org/wiki/Torchwood) yn diweddar (cystadleuwr am shoe teledu gorau erioed), sef spin-off ffuglen wyddonol 'ar gyfer oedolion' o [Doctor Who](https://www.bbc.co.uk/programmes/b006q2x0) (y cystadleuwr arall ar gyfer shoe teledu gorau erioed), wedi'i osod yn benodol yng Nghaerdydd a De Cymru. Mae'r pedwerydd cyfres, a elwir yn "Miracle Day", yn symud y drama i America. Ffuglen wyddonol yw hon, ond y gwyddoeniaeth yn y cyfres hon yw ymchwil gweithredol gofal iechyd.

Y syniad: *un diwrnod mae pob person ar y Ddaear yn peidio marw*.

Mae un is-stori sylweddol o'r gyfres yw gweithio allan sut gall y system gofal iechyd ymdopi â'r 'gwyrth'? Hoffwn ymchwilio ymhellach.

# Twf Poblogaeth

Thema pwysig o'r gyfres yw gorboblogaeth, mae'r teitlau agoriadol yn dangos cyfrif cynyddol o boblogaeth y Ddaear. Mewn pennod un, mae ein arwres Gwen Cooper a'i cyn-cydweithwr heddwas Andy yn trafod sgîl-effaith y gwyrth ar twf poblogaeth:


> **ANDY**: Here we go, look. Planet Earth. On average, three hundred thousand people die every day. So if they stop dying, that's an extra what, million people in just over three days. Add to that five hundred thousand people born every day.
>
> **GWEN**: That's another million every two days plus the first million. Bloody hell.
>
> **ANDY**: That's the fastest population boom in history.
>
> **GWEN**: We're gonna run out of room. 


Ie. Ond mae'r cyfrifiad bras hyn yn gadael allan rhai manylion pwysig: po leiaf y mae pobl yn marw, y fwy gyflym y mae pobl yn cael eu geni. Mae hwn yn enghraifft o system dynamegol, lle mae cyfraddau newid yn dibynnu ar cyflwr y system.

Byddwn yn modelu poblogaeth y Ddaear fel model adrannol: gadewch i $$C$$ bod nifer o blant yn y byd (ni allant cael plant eu hun), gadewch i $$F$$ bod y nifer o oedolion oedran ffrwythlon yn y byd, a gadewch i $$I$$ bod y nifer o oedolion sy'n amhlantadwy oherwydd eu oedran.

Hefyd diffiniwn:

+ $$P = C + F + I$$, poplogaeth y Ddaear,
+ $$g_c$$, y cyfradd y mae plant yn tyfu i mewn i oedolion,
+ $$g_o$$, y cyfradd y mae oedolion yn dod yn amhlantadwy oherwydd eu oedran,
+ $$b$$, y cyfradd geni,
+ $$m$$, y cyfradd marw.

Mae brasamcanion syml yn rhoi $$g_c = \frac{1}{15}$$ (yn ffrwythlon yn 15), $$g_o = \frac{1}{50}$$ (yn amhlantadwy yn 65). Mae [Wicipedia yn rhoi](https://en.wikipedia.org/wiki/Demographics_of_the_world#Age_structure) bod 26% o'r byd yn $$C$$, 9% o'r byd yn $$I$$, ac felly mae 65% o'r byd yn $$F$$. [Mae hefyd yn rhoi taw'r](https://en.wikipedia.org/wiki/Birth_rate) cyfradd geni yw 18.5 genedigaeth i pob mil o bobl, felly'r gyfradd geni aer gyfer $$F$$ yw $$b=0.0285$$; tra bod y gyfradd mawr yw 7.8 pob mil o bobl, felly $$m = 0.0078$$. Mae teitlau agoriadol Torchwood yn rhoi poblogaeth y Ddaear ar dechrau diwrnod y gwyrth fel 6,928,198,257; felly meintiau cychwynnol ein adrannau yw $$C(0) = 1,801,331,547$$, $$F(0) = 4,503,328,867$$, ac $$I(0) = 623,537,843$$.

Sefydlwn ein model adrannol:

$$
\begin{align}
\frac{dC}{dt} &= bF - (m + g_c)C \\
\frac{dF}{dt} &= g_c C - (m + g_o)F \\
\frac{dI}{dt} &= g_o F - m I
\end{align}
$$

Nodwch bod hwn dal yn model syml iawn, nid yw'n ystyried nifer o ffactorau megis erthyliadau, camesgoriadau, na'r gwahanol cyfraddau marw ar gyfer pob categori gwahanol o bobl.

Nawr defnyddiwn y ffwythiant Python `odeint` o `scipy.integrate` i arsylwi'r system dros cyfnod o deng mlwyddyn. Cymharwn byd heb gwyrth $$m = 0.0078$$, gyda diwrnod y gwyrth, $$m = 0$$:

{% highlight python %}
>>> def deilliadau(y, t, cyfradd_marw=0.01):
...     cyfradd_geni = 0.0285
...     gc = 1/15
...     go = 1/50
...     C, F, I = y
...     dCdt = (cyfradd_geni * F) - ((cyfradd_marw + gc) * C)
...     dFdt = (gc * C) - ((cyfradd_marw + go) * F)
...     dIdt = (go * F) - (cyfradd_marw * I)
...     return dCdt, dFdt, dIdt
{% endhighlight %}

{% highlight python %}
>>> from scipy.integrate import odeint
>>> import numpy as np

>>> y0 =(1801331547, 4503328867, 623537843)
>>> t = np.arange(0, (365 * 10) + 0.01, 0.01)

>>> canlyniadau = odeint(deilliadau, y0, t, args=(0.0078,))
>>> C, F, I = canlyniadau.T
>>> P_dimgwyrth = C + F + I

>>> canlyniadau = odeint(deilliadau, y0, t, args=(0,))
>>> C, F, I = canlyniadau.T
>>> P_gwyrth = C + F + I
{% endhighlight %}

Cymharwn `P_dimgwyrth` i `P_gwyrth` a gwelwn effaith y gwyrth ar poblogaeth y Ddaear:

![]({{site.baseurl}}/images/miracle-day-cy.png){: .center-image }

Mae poblogaeth y Ddaear yn dangos twf esbonyddol fel y disgwylir. Yn yr wythnos cyntaf mae poblogaeth y Ddaear yn tyfu gan 0.4 biliwn o bobl, tra bod y rhagolwg 10 blwyddyn yn edrych yn ofnadwy. Gwell i Torchwood sorto rhywbeth allan yn gloi!


# Blaenoriaethu Gwelyau Ysbyty

Mae pawb yn anfarwol, ond nid yw hwn yn golygu bod pobl ddim yn mynd yn sal neu'n anafu. Mae'r ysbytai o day straen enfawr, ac yn gloi mae'n nhw'n gorlawn yn yn rhedeg allan  o gwelyau. Yn yr ail pennod, mewn ysbyty yn Washington DC, mae Doctor Vera Juarez yn sylweddoli yn sydyn eu bod nhw'n blaenoriaethu cleifion yn anghywir:


> **VERA**: Oh my God, we're doing it wrong. Everyone, we're doing it wrong.
>
> **DOCTOR**: We don't have time.
>
> **VERA**: We have nothing but time. Nobody is expectant here. Nobody's gonna die. The first sixty minutes after a trauma, the golden hour? There's no golden hour anymore. All our reflexes are wrong.
>
> **DOCTOR**: I don't understand. What do you want us to do?
>
> **VERA**: Don't you see? Even the worst injured aren't gonna die. So we need to do this backwards. Reverse it. We're desperate for beds so we treat the minor injuries first. If you can get somebody out of here in ten minutes, get them out. Free up the beds for the ones who need help.


Mae hwn i weld yn synhwyrol. Gadewch i ni ymchwilio trwy efelychu'r system o dan y ddau system blaenoriaethu, cyn- ac wedi'r gwyrth.

Defnyddiwn [Ciw](https://ciw.readthedocs.io/cy/latest/) i efelychu ysbyty syml o dau y ddau system blaenoriaethu, cyn y gwyrth lle mae categorïau mwyaf difrifol yn cael eu trin cyn y rhai lleiaf difrifol, ac wedi'i gwyrth lle mae'r rhai lleiaf difrifol yn cael eu trin cyn y fwyaf difrifol. Dywedwn fod pump categori o ddifrifoldeb, mae'r rhai mwyaf difrifol yn cymryd yn hirach i'w trin, ond maent yn cyrraedd yr ysbyty yn llai aml na'r categorïau llai difrifol.

Fel enghraifft, byddwn yn ffugio'r paramedrau:

{% highlight python %}
>>> import ciw
>>> N_cyngwyrth = ciw.create_network(
...     arrival_distributions={
...         'Class 0': [ciw.dists.Exponential(1)],
...         'Class 1': [ciw.dists.Exponential(2)],
...         'Class 2': [ciw.dists.Exponential(4)],
...         'Class 3': [ciw.dists.Exponential(8)],
...         'Class 4': [ciw.dists.Exponential(16)]
...     },
...     service_distributions={
...         'Class 0': [ciw.dists.Exponential(1/5)],
...         'Class 1': [ciw.dists.Exponential(1)],
...         'Class 2': [ciw.dists.Exponential(3)],
...         'Class 3': [ciw.dists.Exponential(12)],
...         'Class 4': [ciw.dists.Exponential(48)]
...     },
...     number_of_servers=[14],
...     priority_classes={
...         'Class 0': 0,
...         'Class 1': 1,
...         'Class 2': 2,
...         'Class 3': 3,
...         'Class 4': 4
...     }
... )
{% endhighlight %}

ac

{% highlight python %}
>>> N_wedigwyrth = ciw.create_network(
...     arrival_distributions={
...         'Class 0': [ciw.dists.Exponential(1)],
...         'Class 1': [ciw.dists.Exponential(2)],
...         'Class 2': [ciw.dists.Exponential(4)],
...         'Class 3': [ciw.dists.Exponential(8)],
...         'Class 4': [ciw.dists.Exponential(16)]
...     },
...     service_distributions={
...         'Class 0': [ciw.dists.Exponential(1/5)],
...         'Class 1': [ciw.dists.Exponential(1)],
...         'Class 2': [ciw.dists.Exponential(3)],
...         'Class 3': [ciw.dists.Exponential(12)],
...         'Class 4': [ciw.dists.Exponential(48)]
...     },
...     number_of_servers=[14],
...     priority_classes={
...         'Class 0': 4,
...         'Class 1': 3,
...         'Class 2': 2,
...         'Class 3': 1,
...         'Class 4': 0
...     }
... )
{% endhighlight %}

Nawr cymharwn pa mor gorlawn yw'r ysbytai trwy cymharu nifer cymedrig o gleifion sydd yn y system dros cyfnod o flwyddyn. Mae hwn yn cymryd bach o waith i'r cyfrifo:

{% highlight python %}
>>> import pandas as pd
>>> def cael_maint_torf(N):
...     Q = ciw.Simulation(N)
...     Q.simulate_until_max_time(400)
...     recs = Q.get_all_records()
...     pobl_wrth_cyrraedd = [(r.arrival_date, r.queue_size_at_arrival + 1) for r in recs]
...     pobl_wrth_gadael = [(r.exit_date, r.queue_size_at_departure) for r in recs]
...     torf = sorted(pobl_wrth_cyrraedd + pobl_wrth_gadael, key=lambda x: x[0])
...     torf_df = pd.DataFrame(
...         {"dyddiad": [x[0] for x in torf], "pobl": [x[1] for x in torf]}
...     )
...     torf_df["cyfwng dyddiad"] = torf_df["dyddiad"].diff()
...     torf_df = torf_df[torf_df["dyddiad"] >= 35]
...     return (torf_df["cyfwng dyddiad"] * torf_df["pobl"]).sum() / 365
{% endhighlight %}

ac er mwyn ystyried amrywiant byddwn yn rhedeg 25 treial o pob system:

{% highlight python %}
>>> def cael_maint_torf_cymedrig(N):
...     meintiau_torf = []
...     for treial in range(25):
...         ciw.seed(treial)
...         meintiau_torf.append(cael_maint_torf(N))
...     return sum(meintiau_torf) / len(meintiau_torf)
{% endhighlight %}

Nawr, cyn y gwyrth, o dan blaenoriaethu normal (trin y cleifion mwyaf difrifol yn gyntaf), cawn:

{% highlight python %}
>>> cael_maint_torf_cymedrig(N_cyngwyrth)
15.093945104963574
{% endhighlight%}

sef 15.1 claf yn yr ysbyty ar cyfartaledd. Ac wedi'r gwyrth, o dan y blaenoriathu newydd (trin y lleiaf difrifol yn gyntaf), cawn:

{% highlight python %}
>>> cael_maint_torf_cymedrig(N_wedigwyrth)
9.930771001044622
{% endhighlight %}

sef 9.9 claf yn yr ysbyty ar cyfartaledd. Felly mae cynnig Vera yn gweithio! O dan y system blaenoriathu newydd mae'r ysbyty llai gorlawn. Wrth gwrs, pan mae neb yn mawr bydd y galw yn cynyddu'n gwirion ta beth, felly mae dal angen i Torchwood achub y dydd!
