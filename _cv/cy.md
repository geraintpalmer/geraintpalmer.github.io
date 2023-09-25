---
layout: page
title: CV
permalink: cv/cy/
---

<div style="text-align: right; font-size: large;">
  <a href="/cv/">Fersiwn Saesneg <img class="emoji" draggable="false" src="https://twemoji.maxcdn.com/2/svg/1f1ec-1f1e7.svg"/></a>
</div>

## Apwyntiadau

Medi 2019 - : **Darlithydd Cyfrwng Cymraeg** yn Ysgol Mathemateg Prifysgol Caerdydd

* Arwain modiwlau, dosbarthiadau enghreifftiol, darlithoedd a thiwtorialau (gweler [Dysgu](/teaching/))
+ Aelod y [grŵp Ymchwil Gweithrediadol](https://www.cardiff.ac.uk/research/explore/research-units/operational-research)

2017 - 2019: **Cynorthwy-ydd Addysgu Cyfrwng Cymraeg** yn Ysgol Mathemateg Prifysgol Caerdydd

+ Arwain modiwlau, cymryd tiwtorialau, dosbarthiadau enghreifftiol, a labiau
+ Cyfieithu adnoddau addysgu
+ Darpariaeth cyfrwng Cymraeg yn y gwasanaeth Cefnogaeth Mathemateg
+ Cefnogi digwyddiadau allanol FMSP


## Addysg

Hyd 2014 - Tach 2018: **PhD mewn Modelu Stocastig Cymhwysol, Prifysgol Caerdydd.**

* Goruchwylwyr: Yr Athro Paul Harper & Dr. Vincent Knight
* Wedi'i chyd-ariannu gan [ABUHB](http://www.wales.nhs.uk/sitesplus/866/home) a Phrifysgol Caerdydd.
* Modelu llifoedd cleifion & gweithio wrth ryngwyneb sefydliad gofal iechyd.
* Modelu llwyrglo yn rhwydweithiau ciwio gan ddefnyddio modelau Markov ac efelychiad cyfrifiadurol.
* Datblygu pecyn meddalwedd ffynhonnell agored, [Ciw](http://ciw.readthedocs.io/), a ddefnyddir yn rhyngwladol.
* Teitl: [*Modelling Deadlock in Queueing Systems*](http://orca.cf.ac.uk/117490/).


Hyd 2013 - Hyd 2014: **MSc Ymchwil Weithrediadol ac Ystadegaeth Gymhwysol, Prifysgol Caerdydd.** Rhagoriaeth.

* Pynciau yn cynnwys: theori ciwio, theori Gemau, technegau ystadegol, cyfresi amser, rhaglennu mathemategol, dulliau hewristig.
* Cwblhau'r traethawd hir ym Mhrifysgol Twente ar leoliad Erasmus.
* Teitl traethawd hir: *Optimising surgery schedules in order to increase operating room utilisation and level beds in the PACU and holding area.*

Medi 2010 - Mai 2013: **BSc Mathemateg, Prifysgol Aberystwyth.** Anrhydedd Dosbarth Cyntaf.



## Cyhoeddiadau
<ul>
{% for pub in site.data.publications %}
  {% if pub.journal == 'NA' %}
    <li>{{ pub.year }}: <b>{{ pub.title }}</b><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<i>{{ pub.authors }}</i> <a class="page-link" href="{{ pub.link }}">O dan adolygiad, ar arXiv.</a></li>
  {% else %}
    {% if pub.multilang == 'no' %}
    <li>{{ pub.year }}: <b>{{ pub.title }}</b><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<i>{{ pub.authors }}</i> <a class="page-link" href="{{ pub.link }}">{{ pub.journal }}</a>
    </li>
    {% elsif pub.lang == 'cy'%}
    <li>{{ pub.year }}: <b>{{ pub.title }}</b> <a class="page-link" href="{{ pub.altlink }}">(en)</a><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<i>{{ pub.authors }}</i> <a class="page-link" href="{{ pub.link }}">{{ pub.journal }}</a>
    </li>
    {% endif %}
  {% endif %}
{% endfor %}
</ul>

## Llyfr

<ul>
{% for book in site.data.books %}
  <li>{{ book.year }}: <b>{{ book.title }}</b><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<i>{{ book.authors }}</i> <a class="page-link" href="{{ book.link }}">{{ book.publisher}}, ISBN: {{ book.isbn }}</a>
  </li>
{% endfor %}
</ul>


## Cyllido & Phrosiectau

<ul>
{% for proj in site.data.proj %}
  {% if proj.amount != 'na' %}
  <li>
  <b>{{ proj.year }}</b> - <i>{{ proj.amount }}</i> - {{ proj.corffcyllido }}
  {% if proj.rol != 'na' %}
  - {{ proj.rol }}
  {% endif %}
  - <b>{{ proj.teitl }}</b>
  </li>
  {% endif %}
{% endfor %}
</ul>



## Diddordebau Ymchwil

+ Ymchwil gweithrediadol cymhwysol, yn arbennig mewn gofal iechyd a gwasanaethau cyhoeddus,
+ Efelychiadau stocastig,
+ Modelu stocastig, theori graffiau, a theori ciwio.


## Gobrau

+ [Gwobr Gwerddon](https://gwerddon.cymru/gwobr-gwerddon/gwobr-2023/) ar gyfer yr erthygl gorau yn Gwerddon 2021-2023 - *Rhaglennu llinol amlamcan i ganfod y tîm Pokémon gorau*
+ [Gwobr ar gyfer Crynodeb (egwyddorion wedi'i seilio ar gwerth) Gorau](https://vbhc.nhs.wales/events/proms-annual-research-conference-2022/) yng Nghynhadledd Ymchwil Genedlaethol PROMs 2022 - *PROMs-Based Key Performance Indicators (KPIs) to Evaluate Waiting List Prioritisation Schemes Against Prudent Healthcare Principles*, gyda Dr Robert Palmer.
+ Rhan o [dîm 2021 a enillodd](https://www.cardiff.ac.uk/cy/news/view/2585799-impact-award-for-cardiff-mathematical-modelers) [Medal Effaith Lyn Thomas](https://www.theorsociety.com/membership/awards-medals-and-scholarships/lyn-thomas-impact-medal/) am waith modelu gyda'r GIG.
+ [Enillydd 2018](https://www.cardiff.ac.uk/cy/news/view/1764522-best-operational-research-phd-thesis-in-in-the-uk-for-school-of-maths-lecturer) o [Wobr Doethurol y Cymdeithas Ymchwil Gweithrediadol](https://www.theorsociety.com/what-we-do/awards-medals-and-scholarships/the-doctoral-award/) ar gyfer "Corff o Ymchwil Mwyaf Nodedig yn arwain at Doethuriath ym maes Ymchwil Gweithrediadol" - *Modelling Deadlock in Queueing Systems*
+ Enillydd 2016 poster gorau yng Nghynhadledd Wyddonol y CCC, Aberystwyth - *Llwyrglo yn Rhwydweithiau Ciwio*


## Dysgu

* Dirprwy Cyfarwyddwr Dysgu ac Addysgu ar gyfer yr Ysgol Mathemateg yng Nghaerdydd (2022-)
* Cymrawd AdvanceHE (FHEA)
* Dosbarthiadau enghreifftiol, darlithoedd a thiwtorialau (gweler [Dysgu](/teaching/)).
* Arwain sesiynau labiau cyfrifiadur (Python, Simul8, LaTeX, Vensim, Excel) ar gyfer israddedigion & myfyrwyr gradd meistr.
* Tiwtor cefnogaeth mathemateg ac ystadegaeth.
* Cyfieithu adnoddau pedagogaidd o Saesneg i Gymraeg.
* Cynhyrchu adnoddau dysgu newydd yn Gymraeg ac yn Saesneg.
* Cyfrannwr allweddol yn fenter datblygiad rhyngwladol arloesol, trwy arwain sesiynau dysgu actif ym Mhrifysgol Namibia (o dan nawdd [Prosiect Phoenix Prifysgol Caerdydd](http://www.cardiff.ac.uk/about/our-profile/our-values/engagement/transforming-communities/the-phoenix-project)).
+ Goruchwylio myfyrwyr prosiect Haf a leoliad Nuffield.


## Adeiladu Cymdeithasau & Threfnu

* Aelod o [Gymdeithas Ymchwil Weithrediadol y DU](https://www.theorsociety.com) & chyn-cadair [SWORDS](http://www.theorsociety.com/Pages/Regional/swords.aspx) (Cymdeithas Trafodaeth Ymchwil Gweithrediadol De Cymru.)
* Aelod o bwyllgor trefnu [DjangoCon Ewrop 2015, Caerdydd](http://2015.djangocon.eu/).
* Aelod gweithredol o [PyDiff](http://www.pydiff.wales/), grŵp cyfarod Python Caerdydd.
* Gwirfoddolwr a chyfrannwr rheolaidd yn PyCon Namibia (o dan nawdd [Prosiect Phoenix Prifysgol Caerdydd](http://www.cardiff.ac.uk/about/our-profile/our-values/engagement/transforming-communities/the-phoenix-project)).
* Profiad trefnu ffrydoedd cynhadledd a helpu trefnu cynhadleddau (Young OR 19, Gweithdy Cydweithio'r SSI 2018).
* Un o drefnwyr [Gweithdu Datblygu Meddalwedd Ymchwil](https://vknight.org/rsd/) blynyddol ar gyfer myfyrwyr PhD yr Ysgol Mathemateg.
* Wedi arwain nifer o ddigwyddiadau estyn ar gyfer disgyblion ysgol o bob oedran (o flynyddoedd 5 i 13) yn Saesneg ac yn Gymraeg.
* Wedi datblygu ac arwain [cwrs codio](/outreach/) Haf ar gyfer plant 11-15 ar gyfer yr [Urdd](https://www.urdd.cymru/cy/).
* Datblygu ac arwain  y modiwl ["Dadansoddi Data gyda Python ac R"](https://www.porth.ac.uk/cy/collection/dadansoddi-data-gydag-r-a-python) ar gyfer rhaglen hyfforddiant PhD y [Coleg Cymraeg Cenedlaethol](https://www.colegcymraeg.ac.uk/cy/).


## Sgiliau

**Meddalwedd:**  Python, LaTeX, Excel, SPSS, R, Simul8, rheolaeth fersiwn gyda Git a GitHub.

**Ieithoedd:** Cymraeg (Rhygl), Saesneg (Rhygl).



## Datblygu Meddalwedd

* Prif ddatblygwr a chynhaliwr [Ciw](https://github.com/CiwPython/Ciw) ([ciw.readthedocs.io](http://ciw.readthedocs.io/)), llyfrgell Python ar gyfer efelychu rhwydweithiau ciwio.
* Profiad defnyddio technegau datblygu meddalwedd modern: rheolaeth fersiwn, profion awtomatig, integreiddiad parhaus.
* Cyfrannwr i'r prosiect ffynhonnell agored [Axelrod](https://github.com/Axelrod-Python/Axelrod).


## Cyrsiau a Fynychwyd

* Cwrs Ragarweiniol ar gyfer Darlithwyr Newydd yn y Gwyddorau Mathemategol yr [IMA](https://ima.org.uk/11361/induction-course-for-new-lecturers-in-the-mathematical-sciences-2019/) - Prifysgol Caergrawnt 2019
* [Cymdeithas Ymchwil Weithrediadol y DU](http://www.theorsociety.com/) - Gweithdy Ymchwilwyr Gyrfa Cynnar - Prifysgol Lancaster 2018
* [Cymraeg i Oedolion](https://welshforadults.cardiff.ac.uk/cy) - Gloywi Iaith CDH001 (Gramadeg) - Prifysgol Caerdydd 20717/18 (Cyfrwng Cymraeg)
* Cwrs Sgiliau Addysgu y [Coleg Cymraeg Cenedlaethol](http://www.colegcymraeg.ac.uk/cy/) - Prifysgol Aberystwyth 2017 (Cyfrwng Cymraeg)
* Ysgol Haf PhD [CHOIR](https://www.utwente.nl/en/choir/) ar Ymchwil Gweithrediadol Gofal Iechyd - Prifysgol Twente 2017
* [NATCOR](http://www.natcor.ac.uk) Rhagolygu & Dadansoddiad Rhagfynegol - Prifysgol Lancaster 2016
* [NATCOR](http://www.natcor.ac.uk) Optimeiddiaeth Amgrwm - Prifysgol Caeredin 2016
* Rhaglen Sgiliau Ymchwil y [Coleg Cymraeg Cenedlaethol](http://www.colegcymraeg.ac.uk/cy/) - Prifysgol Llambed 2015 (Cyfrwng Cymraeg)
* [NATCOR](http://www.natcor.ac.uk) Optimeiddiaeth Cyfuniadol - Prifysgol Southampton 2015
* [NATCOR](http://www.natcor.ac.uk) Efelychiad Cyfrifiadurol - Prifysgol Loughborough 2015
* Cwrs Cloddio Data - Prifysgol Caerdydd 2015
* [NATCOR](http://www.natcor.ac.uk) Modelu Stocastig - Prifysgol Lancaster 2015



## Cyflwyniadau

Siaradwr dwyieithog. Profiad rhyngwladol. Pynciau technegol.
Cynulleidfaoedd amryw gan gynnwys y cyhoedd, academyddion, ymarferwyr gofal iechyd, ac aelod o'r llywodraeth Cymraeg.

+ Medi 2023 - PyCon UK 2023, Caerdydd - *Multi-Objective Linear Programming to find the Best Pokémon Team*
+ Gorff 2023 - ORAHS 2023, Graz - *Evaluating Heterogeneous Ambulance Fleet Allocations in Jakarta*
+ Meh 2022 - Cynhadledd Ymchwil Genedlaethol PROMs 2022 - *PROMs-Based Key Performance Indicators (KPIs) to Evaluate Waiting List Prioritisation Schemes Against Prudent Healthcare Principles*
+ Chwef 2021 - Darlith Beale y Gymdeithas YG 2021 - *Open-Source Simulation with Ciw*
+ Tach 2020 - Symposiwm Academaidd Technolegau Iaith Cymru 2020 - *Mewnblaniadau Geiriau ar gyfer y Gymraeg*
+ Awst 2019 - Ail Diwrnod Arloesi'r ABCi, Bae Caerdydd - *Using Python for Healthcare Modelling*
* Medi 2018 - OR60, Lancaster - Poster: *Ciw: An open source discrete event simulation library*
* Meh 2018 - Cynhadledd Wyddonol y CCC, Aberystwyth - *Dulliau ac Offerynnau ar gyfer Ymchwil Ailgynhyrchiadwy*
* Ebrill 2018 - 3MT yr Ysgol Mathemateg, Caerdydd ([2ail](https://siamukie.wordpress.com/2018/05/01/cardiff-siam-ima-three-minute-thesis-competition/))
* Marw 2018 - STEM for Britain, Llundain - Poster: *Modelling Deadlock in Open Resticted Queueing Networks*
* Chwef 2018 - PyCon Namibia, Windhoek - *Agent Based Modelling with Python*
* Hyd 2017 - PyCon UK, Caerdydd - *Python for Operational Research in Healthcare*
* Ebrill 2017 - IMA and OR Society Conference on Mathematics of Operational Research, Aston - *Queueing networks, Deadlock and Healthcare*
* Chwef 2017 - PyCon Namibia, Windhoek - *Producing Pretty Plots in Python*
* Medi 2016 - PyCon UK, Caerdydd - *Queueing and Python: pip install ciw*
* Mai 2016 - CORS 2016, Banff - *Deadlock in Queueing Networks*
* Mai 2016 - Cynhadledd Wyddonol y CCC, Aberystwyth - Poster: *Llwyrglo yn Rhwydweithiau Ciwio* (Ennillydd poster gorau)
* Maw 2016 - 8th IMA International Conference on Quantitative Modelling in the Management of Health and Social Care, Llundain - *Using Queueing Networks Modelling to Assess the Impact of the OPICP*
* Ion 2016 - PyCon Namibia, Windhoek - *Simulating Queues with Ciw*
* Medi 2015 - Young OR 19, Aston - *Queueing Networks for a Healthcare System, Deadlocking & Reinforcement Learning*
* Gorff 2015 - EURO 2015, Glasgow - *Queueing Networks for a Healthcare System Deadlocking, Reinforcement Learning & Workforce Planning*
* Chwef 2015 - Python Namibia 2015, Windhoek - *Playing with Reinforcement Learning in Python*


## Ymddangosiadau yn y Cyfryngau

* 06/11/2020 - **Yfory Newydd** - *BBC Radio Cymru*
* 08/07/2022 - **Talk Python Podcast** - ([Applied mathematics with Python](https://talkpython.fm/episodes/show/372/applied-mathematics-with-python))
* 04/01/2023 - **Rhaglen Aled Hughes** (Pokémon a'r NHS) - *BBC Radio Cymru*


## Cyswllt

E-bost: palmergi1@cardiff.ac.uk

Geirdaon ar gael ar gais.