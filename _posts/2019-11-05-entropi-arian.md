---
layout     : post
title      : "Cymhlethdod Darnau Arian"
language   : cymraeg
comments   : true
---

Gwnes i anghytuno gyda fy nhad cu dros y penwythnos.
Mae e'n mynnu bod ['hen arian'](https://en.wikipedia.org/wiki/%C2%A3sd) (cyn-degoli) lot symlach na'n system degol modern.
A dwi'n ei weld mor dryslyd!
Meddyliais, rhaid bod ffordd o mesur hyn.

Ystyriaf tree system arian fan hyn (fel ffracsiynau o'u darn arian mwyaf):

+ 'Hen arian', hynny yw punnoedd Prydeinig cyn-degoli gyda'r darnau arian canlynol: ceiniog (1d), tair ceiniog (3d), chwecheiniog (6d), swllt (12d), deuswllt (24d), hanner coron (30d), coron (60d), a sofran (£1 neu 240d);[^1]
+ Euros (neu'r punt Prydeinig ôl-degoli, gan fod gennyn nhw yr un gwerthoedd bach) gyda'r darnau arian canlynol: 1c, 2c, 5c, 10c, 20c, 50c, ac €1 neu 100c;
+ Doleri Americanaidd gyda'r darnau arian canlynol: senten (1¢), nicel (5¢), dimai (10¢), chwarter (25¢), hanner-doler (50¢), a doler ($1 neu 100¢).

Byddaf yn cymharu rhain mewn tri dimensiwn: *effeithlonrwydd*, *cymhlethdod*, ac *argaeledd*. Byddai'n defnyddio 'brute-force' i gwerthuso rhain, gan ddefnyddio `itertools` a `pandas` yn Python er mwyn dadansoddi'r hoff cyfuniadau darnau arian yn is na gwerth darn arian mwyaf y cylchrediad.


# Effeithlonrwydd

Pos mathemategol cyffredin yw'r [problem creu-newid](https://en.wikipedia.org/wiki/Change-making_problem). Hynny yw, ar gyfer rhyw gwerth o arian, beth yw'r nifer lleiaf o darnau arian sydd angen er mwyd creu'r gwerth hyn.
Gallwn datrys hyn trwy rhaglennu llinol neu rhaglennu dynamig, ond fan hyn defnyddiaf dull 'brute-force'.
Ar gyfer pob gwerth posib yn is na'u darn arian mwyaf, cawn:

![]({{site.baseurl}}/images/efficiency-cy.png){: .center-image }

Euros yw'r cylchrediad mwyaf effeithlon o bell ffordd, gydag arian Prydeinig cyn-degoli y lleiaf effeithlon.


# Argaeledd

Fan hyn roeddwn eisiau mesur 'robustness' cylchrediad i rhedeg allan o rhyw gwerth darn arian, a dechreuais i ystyried y pos mathemategol enwog [problem darnau arian Frobenius](https://en.wikipedia.org/wiki/Coin_problem) (a elwir hefyd y problem McNugget), pan mae rhai gwerthoedd darn arian wedi ei symud o'r set.
Mae hwn yn problem anodd, er gall cael ei datrys trwy defnyddio 'brute-force' yn yr achosion hyn.

Symleiddiais i'r problem trwy ofyn y cwestiwn tebyg o ba canran o'r holl gwerthoedd posib allai gwneud allan o $$n$$ darn arian?
Cawn:

![]({{site.baseurl}}/images/availability-cy.png){: .center-image }

Mae gan euros argaeledd lot fwy uchel na'r doler, sydd yn ei tro yn cael argaeledd mwy na'r darnau arian Prydeinig cyn-degoli.


# Cymhlethdod

Betholygodd fy nhad cu gan 'symlach'?
Sai'n siwr, ond gallwn mesur cymhlethdod trwy ystyried arian fel problem tebygolrwydd:
tybiwch bod yna nifer anfeidraidd hafal o darnau arian o bob werth.
Gadewch i $$N$$ a $$V$$ bod yn hapnewidynau yn cynrychioli nifer o darnau arian a ddewisir ar hap, a gwerth i'w sicrhau, yn ôl eu trefn.
Gadewch i $$\mathbb{P}(N=n, V=v)$$ bod y tebygolrwydd o cael gwerth $$v$$ pan ddewisir $$n$$ darn arian ar hap.

Gallwn mesur [*entropi Shannon*](https://en.wikipedia.org/wiki/Entropy_(information_theory)) pob dosraniad ymylol:

$$S_n = -\sum_v \mathbb{P}(V=v | N=n) \log_2 \mathbb{P}(V=v | N=n)$$

$$S_v = -\sum_n \mathbb{P}(N=n | V=v) \log_2 \mathbb{P}(N=n | V=v)$$

Gallwn meddwl am hyn fel rhyw mesur fel amrywiant, ond ar gyfer data enwol (enwol fan hyn gan nad ydyn yn poeni am pa mor bell mae'r gwerthoedd/niferoedd o'u gilydd, ond eu bod yn wahanol).

Cawn:

![]({{site.baseurl}}/images/complexity-cy.png){: .center-image }

Fan hyn y doler Americanaidd yw'r lleiaf cymhleth, wedi'i ddilyn yn agos gan y Euro.
Arian Prydeinig cyn-degoli sydd a'r mwyaf o cymhethdod o'r tri.

Gallwn hefyd mesur [*cyd-entropi*](https://en.wikipedia.org/wiki/Joint_entropy) y dosraniad:

$$H(N, V) = -\sum_n \sum_v \mathbb{P}(N=n, V=v) \log_2 \mathbb{P}(N=n, V=v)$$

Wedi mesur ar y cyd, yr Euro sy'n dod allan fel y cylchrediad symlaf (jest), gyda $$H(N, V) = 11.44$$, yna'r doler Americanaidd gyda $$H(N, V) =  11.53$$, ac yn olaf arian Prydeinig cyn-degoli gyda $$H(N, V) =  13.40$$.

Yn gyfangwbl, arian Prydeinig cyn-degoli yw'r lleiaf effeithlon, lleiaf argael, a mwyaf cymhleth o'r tri cylchrediad a chymharir, yn cyfiawnhau fy nryswch.


# Beth am Gringotts?

Dyfeisiodd JK Rowling cylchrediad eithaf od [yn parodïo cymhlethdod arian Prydeinig cyn-degol](https://en.wikipedia.org/wiki/%C2%A3sd#In_popular_culture).
Felly cymharais i hwn.

+ Mae arian dewinod yn cynnwys 'knuts', 'sickles', a 'galleons', gyda 29 'knut' i bob 'sickle', ac 17 'sickle' i bob 'galleon'.

Wrth cymharu i'r tri arall:

![]({{site.baseurl}}/images/gringotts-cy.png){: .center-image }

Mae hwn yn diddorol! Mae arian dewinod angen lot mwy o darnau arian (felly mae llai effeithlon), ac mae ganddo argaeledd lot llai na'r tri cylchrediad arall.
Serch hynny mae ganddo entropïau ymylol llai (a chyd-entropi gymharol cymedrig, $$H(N, V) = 12.12$$).

Pam mae arian dewinod yn ymddwyn mor wahanol i'r arian eraill?
Mae un gwahaniaeth mawr rhwng arian dewinod a'r tri arall a chymharwyd fan hyn: mae pob gwerth darn arian mewn arian dewinod yn lluosymiau o'r lleill.
Mae gan y systemau eraill o leiaf un pâr o werthoedd darn arian nad yw'n luosymiau o'u gilydd: dimai a chwarter (10¢ a 25¢), 20c a 50c, a nifer mewn hen arian Prydeinig, e.e. deuswllt a hanner coron (24d a 30d).
Gall hyn fod yn un achos o cymhlethdod mewn darnau arian.


---

[^1]: roedd hefyd dimai (½d), ffyrling (¼d), a hanner sofran (120d), ond gadawais i rhain allan fan hyn er mwyn arbed cymhlethdod cyfrifiannol.