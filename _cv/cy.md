---
layout: page
title: CV
permalink: cv/cy/
---

[In English](/cv/)

## Apwyntiadau

Medi 2017 - : **Cynorthwy-ydd Addysgu Cyfrwng Cymraeg** yn Ysgol Mathemateg Prifysgol Caerdydd

+ Dosbarthiadau enghreifftiol a thiwtorialau cyfrwng Cymraeg
+ Cyfieithu adnoddau addysgu
+ Darpariaeth cyfrwng Cymraeg yn Maths Support


## Addysg

Hyd 2014 - Tach 2018: **PhD mewn Modelu Stocastig Cymhwysol, Prifysgol Caerdydd.**

* Goruchwylwyr: Yr Athro Paul Harper & Dr. Vincent Knight
* Wedi'i chyd-ariannu gan [ABUHB](http://www.wales.nhs.uk/sitesplus/866/home) a Phrifysgol Caerdydd.
* Modelu llifoedd cleifion & gweithio wrth ryngwyneb sefydliad gofal iechyd.
* Modelu llwyrglo yn rhwydweithiau ciwio gan ddefnyddio modelau Markov ac efelychiad cyfrifiadurol.
* Datblygu pecyn meddalwedd ffynhonnell agored, [Ciw](http://ciw.readthedocs.io/), a ddefnyddir yn rhyngwladol.
* Teitl: *Modelling Deadlock in Queueing Systems.*


Hyd 2013 - Hyd 2014: **MSc Ymchwil Weithrediadol ac Ystadegaeth Gymhwysol, Prifysgol Caerdydd.** Rhagoriaeth.

* Pynciau yn cynnwys: theori ciwio, theori Gemau, technegau ystadegol, cyfresi amser, rhaglennu mathemategol, dulliau hewristig.
* Cwblhau'r traethawd hir ym Mhrifysgol Twente ar leoliad Erasmus.
* Teitl traethawd hir: *Optimising surgery schedules in order to increase operating room utilisation and level beds in the PACU and holding area.*

Medi 2010 - Mai 2013: **BSc Mathemateg, Prifysgol Aberystwyth.** Anrhydedd Dosbarth Cyntaf.



## Cyhoeddiadau
<ul>
{% for pub in site.data.publications %}
  <li>{{ pub.year }}: <b>{{ pub.title }}</b> <i>{{ pub.authors }}</i> 
  	{% if pub.published == 'yes' %}
  	  <a class="page-link" href="{{ pub.link }}">{{ pub.journal }}</a>
  	{% elsif pub.preprint == 'yes' %}
  	  Dan Adolygiad. <a class="page-link" href="{{ pub.link }}">{{ pub.arxiv }}</a>
  	{% else %}
  	  Dan Adolygiad.
  	{% endif %}
  </li>
{% endfor %}
</ul>


## Dysgu

* Dosbarthiadau enghreifftiol, darlithoedd a thiwtorialau (gweler [Dysgu](/teaching/)).
* Arwain sesiynau labiau cyfrifiadur (Python, Simul8, LaTeX, Vensim, Excel) ar gyfer israddedigion & myfyrwyr gradd meistr.
* Tiwtor cefnogaeth mathemateg ac ystadegaeth.
* Cyfieithu adnoddau pedagogaidd o Saesneg i Gymraeg.
* Cynhyrchu adnoddau dysgu newydd yn Gymraeg ac yn Saesneg.
* Cyfrannwr allweddol yn fenter datblygiad rhyngwladol arloesol, trwy arwain sesiynau dysgu actif ym Mhrifysgol Namibia (gyda [Prosiect Phoenix Prifysgol Caerdydd](http://www.cardiff.ac.uk/about/our-profile/our-values/engagement/transforming-communities/the-phoenix-project)).



## Adeiladu Cymdeithasau & Threfnu

* Aelod o [Gymdeithas Ymchwil Weithrediadol y DU](https://www.theorsociety.com) & cadair bwyllgor [SWORDS](http://www.theorsociety.com/Pages/Regional/swords.aspx) (Cymdeithas Trafodaeth Ymchwil Gweithrediadol De Cymru.)
* Aelod o bwyllgor trefnu [DjangoCon Ewrop 2015, Caerdydd](http://2015.djangocon.eu/).
* Aelod gweithredol o [PyDiff](http://www.pydiff.wales/), grŵp cyfarod Python Caerdydd.
* Gwirfoddolwr a chyfrannwr rheolaidd yn PyCon Namibia (gyda [Prosiect Phoenix Prifysgol Caerdydd](http://www.cardiff.ac.uk/about/our-profile/our-values/engagement/transforming-communities/the-phoenix-project)).




## Datblygu Meddalwedd

* Prif ddatblygwr a chynhaliwr [Ciw](https://github.com/CiwPython/Ciw) ([ciw.readthedocs.io](http://ciw.readthedocs.io/)), llyfrgell Python ar gyfer efelychu rhwydweithiau ciwio.
* Profiad defnyddio technegau datblygu meddalwedd modern: rheolaeth fersiwn, profion awtomatig, integreiddiad parhaus.
* Cyfrannwr i'r prosiect ffynhonnell agored [Axelrod](https://github.com/Axelrod-Python/Axelrod).



## Cyflwyniadau

Siaradwr dwyieithog. Profiad rhyngwladol. Pynciau technegol.
Cynulleidfaoedd amryw gan gynnwys y cyhoedd, academyddion, ymarferwyr gofal iechyd, ac aelod o'r llywodraeth Cymraeg.

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


## Sgiliau

**Meddalwedd:**  Python, LaTeX, Excel, SPSS, Simul8, rheolaeth fersiwn gyda Git a GitHub.

**Ieithoedd:**  Saesneg (Rhygl), Cymraeg (Rhygl).


## Cyllidau

+ 2018 - [Grant Bach y Coleg Cymraeg](http://www.colegcymraeg.ac.uk/cy/ycoleg/prosiectau/grantiaubach/) (Creu adnoddau aml-gyfrwng rhaglennu cyfrwng Cymraeg) -  £2,500
+ 2017 - Cymrodoriaeth y [Sustainable Software Institute](https://www.software.ac.uk/) - £3,000



## Cyrsiau a Fynychwyd

* [Cymdeithas Ymchwil Weithrediadol y DU](http://www.theorsociety.com/) - Gwiethdy Ymchwilwyr Gyrfa Cynnar - Prifysgol Lancaster 2018
* [Cymraeg i Oedolion](https://welshforadults.cardiff.ac.uk/cy) - Gloywi Iaith CDH001 (Gramadeg) - Prifysgol Caerdydd 20717/18 (Cyfrwng Cymraeg)
* Cwrs Sgiliau Addysgu y [Coleg Cymraeg Cenedlaethol](http://www.colegcymraeg.ac.uk/cy/) - Prifysgol Aberystwyth 2017 (Cyfrwng Cymraeg)
* Ysgol Haf PhD [CHOIR](https://www.utwente.nl/en/choir/) ar Ymchwil Gweithrediadol Gofal Iechyd - Prifysgol Twente 2017
* [NATCOR](http://www.natcor.ac.uk) Rhagolygu & Dadansoddiad Rhagfynegol - Prifysgol Lancaster 2016
* [NATCOR](http://www.natcor.ac.uk) Optimeiddiaeth Amgrwm - Prifysgol Caeredin 2016
* Rhaglen Sgiliau Ymchwil y [Coleg Cymraeg Cenedlaethol](http://www.colegcymraeg.ac.uk/cy/) - Prifysgol Llambed 2015 (Cyfrwng Cymraeg)
* [NATCOR](http://www.natcor.ac.uk) Optimeiddiaeth Cyfuniadol - Prifysgol Southampton 2015
* [NATCOR](http://www.natcor.ac.uk) Efelychiad Cyfrifiadurol - Prifysgol Loughborough 2015
* Cwrs Cloddio - Prifysgol Caerdydd 2015
* [NATCOR](http://www.natcor.ac.uk) Modelu Stocastig - Prifysgol Lancaster 2015



## Cyswllt

E-bost: palmergi1@cardiff.ac.uk

Geirdaon ar gael ar gais.