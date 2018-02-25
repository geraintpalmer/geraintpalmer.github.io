---
layout     : post
title      : "Beth yw'r siawns o farw mewn damwain hewl cyn troi 100?"
language   : cymraeg
comments   : true
---

Fe wnaeth cyfrifiad cefn amlen, wedi'i thanio o sgwrs bwrdd cinio yn Windhoek yr
wythnos yma, amcangyfrif bod y siawns ohonof i'n marw o ddamwain hewl cyn i mi droi'n
can mlwydd oed tua 0.00498.
Hynny yw tua un mewn pob 200 o bobl.
Yn y blog yma fe wnâi trio gwella cywirdeb y cyfrifiad yma.

Y rheswm oeddwn i wrth y bwrdd cinio oedd i fynychu'r gynhadledd
[PyCon Namibia 2018](https://na.pycon.org/en/) llwyddianus, cefnogwyd hwn yn
hael gan [Brosiect Phoenix](http://www.cardiff.ac.uk/phoenix-project) Prifysgol
Caerdydd.
Wrth y ford roedd yna fathemategwyr, gwyddonwyr ddaear, anaesthetegyddion,
rhaglennwr cyfrifiaduron ac athronydd, pan berwyd y cwestiwn canlynol:
"Pob blwyddyn mae 1 mewn 20,000 o bobl yn marw mewn damwain hewl ym Mhrydain,
beth yw'r tebygolrwydd o farw mewn damwain hewl cyn troi'n can mlwydd oed?"

Gadawer i $$p = 1 / 20000$$.
Ystyriwch:

+ Ar ôl 1 blwyddyn o fyw, mae yna debygolrwydd $$p$$ o farw mewn damwain hewl, a
$$(1 - p)$$ o oroesi i fyw am flwyddyn arall.
+ Ar ôl yr ail flwyddyn o fyw, mae yna siawns $$p + (1 - p)p$$ o fod wedi marw
mewn damwain hewl (hynny yw siawns $$p$$ o flwyddyn 1, ar ôl hwnna rydych yn
barod wedi marw, a thebygolrwydd $$(1 - p)$$ o oroesi nes blwyddyn dau, ac yna
tebygolrwydd $$p$$ eto o farw unwaith bod yr oroesiad cyntaf wedi digwydd).
Felly mae siawns $$(1 - p)^2$$ o fod wedi goroesi'r holl ffordd i'r trydydd
blwyddyn.
+ O'r un rhesymeg mae yna siawns $$p + (1 - p)p + (1 - p)^2p$$ o fod wedi marw
mewn damwain hewl erbyn diwedd y trydedd flwyddyn.

Gall tynnu delwedd o hwn fel y goeden tebygolrwydd isod.

![]({{site.baseurl}}/images/tree_diagram1-cy.png)

Ar gyfer 100 cangen, hynny yw 100 blwyddyn o fyw, adiwn holl debygolrwyddau
cangen o farw.
Rhoddir hyn:

$$P(\text{Marw mewn damwain hewl o fewn 100 blwyddyn}) = \sum_{i=0}^{99} (1 - p)^i p$$

Yn y bôn hwn yw'r
[dosraniad Binomial](https://en.wikipedia.org/wiki/Binomial_distribution).
Pan mae $$p = 1 / 20000$$:

$$P(\text{Marw mewn damwain hewl o fewn 100 blwyddyn}) \approx 0.00498$$

# Rhagdybiaethau

Mae'r cyfrifiad uchod yn tybio cwpl o bethau afrealistig:

1. Mae'r tebygolrwydd o farw mewn damwain hewl yn unfath ar gyfer pob oedran.
1. Os nad ydw i'n marw mewn damwain car, ni allaf farw o unrhyw beth arall.

# Newidiadau i'r model

Gan wneud newidiadau mân i'r hafaliad uchod, gallwn ddelio a'r rhagdybiaethau
afrealistig hyn:

$$P(\text{Marw mewn damwain hewl o fewn 100 blwyddyn}) = \sum_{i=1}^{100} \left(\prod_{k=1}^{i}(1 - m_{k-1})\right) p_i$$

lle $$p_i$$ yw'r tebygolrwydd o farw mewn damwain hewl yn $$i^{\text{fed}}$$
blwyddyn eich bywyd, a $$m_i$$ yw'r tebygolrwydd o farw o *unrhyw beth* yn
$$i^{\text{fed}}$$ blwyddyn eich bywyd.
O'r diffiniad yma mae $$m_0 = 0$$ achos ni allwch farw cyn geni.
Dangosir hyn yn y goeden tebygolrwydd sydd wedi'i addasu isod:

![]({{site.baseurl}}/images/tree_diagram2-cy.png)

Fedrir cael y data marwolaeth yma'n agored, wedi'i splitio gan oedran, o'r ONS.
Hefyd fydd data poblogaethau yn ddefnyddiol.
Mae'r setiau data a lawrlwythais i ar gyfer 2016, ond maen nhw ar gyfer Cymru a
Lloegr yn unig.
Mae'r data hefyd yn binio'r oedrannau mewn i grwpiau oedran:

+ [Set data marwolaethau 2016 ar gyfer Cymru a Lloegr](https://www.ons.gov.uk/peoplepopulationandcommunity/birthsdeathsandmarriages/deaths/datasets/deathregistrationssummarytablesenglandandwalesreferencetables)
+ [Set data poblogaeth y DU](https://www.ons.gov.uk/peoplepopulationandcommunity/populationandmigration/populationestimates/datasets/populationestimatesforukenglandandwalesscotlandandnorthernireland)

Ar ôl glanhau'r data, fe ges i:

  | Grŵp Oedran | Poblogaeth | Pob Marwolaeth | Marwolaethau Hewl |
  |-------------|------------|----------------|-------------------|
  | < 1         | 702,448    | 2711           | 0                 |
  | 1 - 4       | 2,899,859  | 433            | 18                |
  | 5 - 14      | 2,899,859  | 525            | 35                |
  | 15 - 24     | 7,132,934  | 2153           | 324               |
  | 25 - 34     | 7,944,899  | 4364           | 296               |
  | 35 - 44     | 7,448,495  | 8550           | 201               |
  | 45 - 54     | 8,190,797  | 21200          | 257               |
  | 55 - 64     | 6,695,865  | 41577          | 180               |
  | 65 - 74     | 5,765,980  | 87556          | 181               |
  | 75 - 84     | 3,342,771  | 148655         | 185               |
  | ≥ 85        | 1,408,727  | 207314         | 87                |
  |-------------|------------|----------------|-------------------|

<br>

Tebygolrwydd mawr pob grŵp yw'r Boblogaeth wedi'i rhannu gan Bob Marwolaeth, a'r
tebygolrwydd marw ar yr hewl yw'r Boblogaeth wedi'i rhannu gan Farwolaethau
Hewl.
Nawr $$m_i$$ yw tebygolrwydd mawr y grŵp oedran mae $$i$$ yn perthyn iddo, a
$$p_i$$ yw'r tebygolrwydd marw ar yr hewl y grŵp oedran mae $$i$$ yn perthyn
iddo.

Pam oes angen y lefel manyldeb yma?
Wel mae'r tebygolrwydd mawr yn sensitif i oedran, mae gan fabanod a'r henoed lot
mwy o risg marw na gweddill y boblogaeth.
Dangosir hyn yn y siart bar isod:

![]({{site.baseurl}}/images/death_age_cy.png)

Tra bod tebygolrwydd marw ar yr hewl, hefyd yn sensitif i oedran, lot fwy uchel
ar gyfer pobl yn ei harddegau ac oedolion ifanc:

![]({{site.baseurl}}/images/roaddeath_age_cy.png)

Nawr yn amnewid y gwerthoedd a chyfrifir ar gyfer yr $$m_i$$'s a'r $$p_i$$ i
fewn i'r hafaliad, cawn debygolrwydd lot fwy cywir o farw:

$$P(\text{Marw mewn damwain hewl o fewn 100 blwyddyn}) = \sum_{i=1}^{100} \left(\prod_{k=1}^{i}(1 - m_{k-1})\right) p_i \approx 0.00255$$

hynny yw tua 1 ym mhob 400 o bobl.

Yn olaf, edrychwn ar $$P(\text{Marw mewn damwain hewl o fewn } x \text{ blwyddyn})$$.
Mae'r plot isod yn dangos hwn wrth i $$x$$ newid.
Gwelwn fod y siawns o farw eithaf isel nes i ni gyrraedd ein harddegau hwyr
(pryd rydym yn dechrau gyrru) ac yna'n cynyddu'n gyson pob blwyddyn.

![]({{site.baseurl}}/images/lifetime_roaddeath_age_cy.png)
