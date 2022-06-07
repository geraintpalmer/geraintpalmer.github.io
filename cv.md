---
layout: page
title: CV
---

<div style="text-align: right; font-size: large;">
  <a href="/cv/cy/">Welsh Version <img class="emoji" draggable="false" src="https://twemoji.maxcdn.com/2/svg/1f3f4-e0067-e0062-e0077-e006c-e0073-e007f.svg"/></a>
</div>

## Appointments

Sept 2019 - : **Welsh Medium Lecturer** at Cardiff University's School of Mathematics

* Leading modules, example classes, lectures and tutorials (see [Teaching](/teaching/))
+ Member of the [Operational Research group](https://www.cardiff.ac.uk/research/explore/research-units/operational-research)

2017 - 2019 : **Welsh Medium Teaching Associate** at Cardiff University's School of Mathematics

+ Leading modules, taking tutorials, example classes, and labs
+ Translation of educational resources
+ Welsh provision at Maths Support
+ Supporting FMSP outreach events


## Education

Oct 2014 - Nov 2018: **PhD in Applied Stochastic Modelling, Cardiff University.**

* Supervisors: Prof. Paul Harper & Dr. Vincent Knight
* Jointly funded by [ABUHB](http://www.wales.nhs.uk/sitesplus/866/home) & Cardiff University.
* Modelling of patient flows & working at the interface of a healthcare organisation.
* Modelling of deadlock in queueing networks using Markov models and discrete event simulation.
* Development of an internationally used open source software package, [Ciw](http://ciw.readthedocs.io/).
* Title: [*Modelling Deadlock in Queueing Systems*](http://orca.cf.ac.uk/117490/).


Oct 2013 - Oct 2014: **MSc Operational Research and Applied Statistics, Cardiff University.** Distinction.

* Taught topics include: queueing theory, game theory, statistical techniques, time series, mathematical programming, heuristics.
* Completed dissertation at the University of Twente on an Erasmus placement.
* Dissertation title: *Optimising surgery schedules in order to increase operating room utilisation and level beds in the PACU and holding area.*

Sept 2010 - May 2013: **BSc Mathematics, Aberystwyth University.** First Class Honours.



## Publications
<ul>
{% for pub in site.data.publications %}
  {% if pub.multilang == 'no' %}
  <li>{{ pub.year }}: <b>{{ pub.title }}</b><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<i>{{ pub.authors }}</i> <a class="page-link" href="{{ pub.link }}">{{ pub.journal }}</a>
  </li>
  {% elsif pub.lang == 'en'%}
  <li>{{ pub.year }}: <b>{{ pub.title }}</b> <a class="page-link" href="{{ pub.altlink }}">(cy)</a><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<i>{{ pub.authors }}</i> <a class="page-link" href="{{ pub.link }}">{{ pub.journal }}</a>
  </li>
  {% endif %}
{% endfor %}
</ul>

## Book

<ul>
{% for book in site.data.books %}
  <li>{{ book.year }}: <b>{{ book.title }}</b><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<i>{{ book.authors }}</i> <a class="page-link" href="{{ book.link }}">{{ book.publisher}}, ISBN: {{ book.isbn }}</a>
  </li>
{% endfor %}
</ul>



## Funding & Projects

<ul>
{% for proj in site.data.proj %}
  {% if proj.amount != 'na' %}
  <li>
  <b>{{ proj.year }}</b> - <i>{{ proj.amount }}</i> - {{ proj.fundingbody }}
  {% if proj.role != 'na' %}
  - {{ proj.role }}
  {% endif %}
  - <b>{{ proj.title }}</b>
  </li>
  {% endif %}
{% endfor %}
</ul>

## Research Interests

+ Applied operational research, in particular healthcare and public services,
+ Stochastic simulation,
+ Stochastic modelling, graph theory, and queueing theory.


## Awards

+ Part of the [2021 team that won](https://www.cardiff.ac.uk/news/view/2585799-impact-award-for-cardiff-mathematical-modelers) the [Lyn Thomas Impact Medal](https://www.theorsociety.com/membership/awards-medals-and-scholarships/lyn-thomas-impact-medal/) for modelling work with the NHS.
+ [2018 Winner](https://www.cardiff.ac.uk/news/view/1764522-best-operational-research-phd-thesis-in-in-the-uk-for-school-of-maths-lecturer) of the [OR Society Doctoral Award](https://www.theorsociety.com/what-we-do/awards-medals-and-scholarships/the-doctoral-award/) for "Most Distinguished Body of Research leading to the Award of a Doctorate in the field of OR" - *Modelling Deadlock in Queueing Systems*
+ 2016 Winner of best poster at the Cynhadledd Wyddonol y CCC, Aberystwyth - *Llwyrglo yn Rhwydweithiau Ciwio*



## Learning & Teaching

* Delivery of example classes, lectures and tutorials (see [Teaching](/teaching/)).
* Leading computer lab sessions (Python, Simul8, LaTeX, Vensim, Excel) for undergraduate & masters students.
* Mathematics & Statistics support tutor.
* Translation of pedagogic material from English to Welsh.
* Production of new learning materials in both English and Welsh.
* Key participant in innovative international development initiative leading active learning sessions at the University of Namibia (under the [Cardiff University Phoenix Project](http://www.cardiff.ac.uk/about/our-profile/our-values/engagement/transforming-communities/the-phoenix-project)).
* Supervision of Summer project and Nuffield placement students.


## Community Building & Organisation

* Member of [the UK OR Society](https://www.theorsociety.com) & former chair of [SWORDS](http://www.theorsociety.com/Pages/Regional/swords.aspx) (South Wales Operational Research Discussion Society).
* Member of organising committee for [DjangoCon Europe 2015, Cardiff](http://2015.djangocon.eu/).
* Active member of [PyDiff](http://www.pydiff.wales/), the Cardiff Python meetup.
* Regular volunteer and participant at PyCon Namibia (under the [Cardiff University Phoenix Project](http://www.cardiff.ac.uk/about/our-profile/our-values/engagement/transforming-communities/the-phoenix-project)).
* Experience of organising conference streams and assisting in conference organisation (Young OR 19, SSI Collaborations Workshop 2018).
* Organiser of a yearly [Research Software Development Workshop](https://vknight.org/rsd/) for PhD students at the School of Mathematics.
* Have lead many outreach activities for school pupils of all ages (from years 5 to 13) in both English and Welsh.
* Developed and lead a Summer [coding course](/outreach/) for 11-15 year olds for the [Urdd](https://www.urdd.cymru/en/).
* Development and leading ["Dadansoddi Data gyda Python ac R"](https://www.porth.ac.uk/cy/collection/dadansoddi-data-gydag-r-a-python) module for the [Coleg Cymraeg Cenedlaethol](https://www.colegcymraeg.ac.uk/en/)'s PhD training programme.


## Skills

**Software:**  Python, LaTeX, Excel, SPSS, R, Simul8, version control with Git and GitHub.

**Languages:**  English (Fluent), Welsh (Fluent).



## Software Development

* Main developer and maintainer of [Ciw](https://github.com/CiwPython/Ciw) ([ciw.readthedocs.io](http://ciw.readthedocs.io/)), a Python library for simulating queueing networks.
* Experience of modern software development techniques: version control, automated testing, continuous integration.
* Contributor to the open source project [Axelrod](https://github.com/Axelrod-Python/Axelrod).


## Courses Attended

* [IMA](https://ima.org.uk/11361/induction-course-for-new-lecturers-in-the-mathematical-sciences-2019/) Induction Course for New Lecturers in the Mathematical Sciences - Cambridge University 2019
* [The OR Society](http://www.theorsociety.com/) - Early Career Researcher Workshop - Lancaster University 2018
* [Welsh for Adults](https://welshforadults.cardiff.ac.uk/) - Gloywi Iaith CDH001 (Grammar) - Cardiff University 2017/18 (Welsh medium)
* [Coleg Cymraeg Cenedlaethol](http://www.colegcymraeg.ac.uk/en/)'s Teaching Skills Course - Aberystwyth University 2017 (Welsh Medium)
* [CHOIR](https://www.utwente.nl/en/choir/) Healthcare Operations Research PhD Summer School - University of Twente 2017
* [NATCOR](http://www.natcor.ac.uk) Forecasting & Predictive Analysis - Lancaster University 2016
* [NATCOR](http://www.natcor.ac.uk) Convex Optimisation - Edinburgh University 2016
* [Coleg Cymraeg Cenedlaethol](http://www.colegcymraeg.ac.uk/en/)'s Research Skills Programme - Lampeter University 2015 (Welsh Medium)
* [NATCOR](http://www.natcor.ac.uk) Combinatorial Optimisation - Southampton University 2015
* [NATCOR](http://www.natcor.ac.uk) Simulation - Loughborough University 2015
* Data Mining - Cardiff University 2015
* [NATCOR](http://www.natcor.ac.uk) Stochastic Modelling - Lancaster University 2015



## Presentations

Bilingual speaker. International experience. Technical topics.
Diverse audiences including general public, academics, healthcare practitioners, and member of the Welsh government.

+ Feb 2021 - OR Society Beale Lecture 2021 - *Open-Source Simulation with Ciw*
+ Nov 2020 - Wales Academic Symposium of Language Technologies 2020 - *Mewnblaniadau Geiriau ar gyfer y Gymraeg*
+ Aug 2019 - Second ABCi Innovation Day, Cardiff Bay - *Using Python for Healthcare Modelling*
* Sept 2018 - OR60, Lancaster - Poster: *Ciw: An open source discrete event simulation library*
* June 2018 - Cynhadledd Wyddonol y CCC, Aberystwyth - *Dulliau ac Offerynnau ar gyfer Ymchwil Ailgynhyrchiadwy*
* April 2018 - School of Mathematics 3MT, Cardiff ([2nd place](https://siamukie.wordpress.com/2018/05/01/cardiff-siam-ima-three-minute-thesis-competition/))
* Mar 2018 - STEM for Britain, London - Poster: *Modelling Deadlock in Open Restricted Queueing Networks*
* Feb 2018 - PyCon Namibia, Windhoek - *Agent Based Modelling with Python*
* Oct 2017 - PyCon UK, Cardiff - *Python for Operational Research in Healthcare*
* April 2017 - IMA and OR Society Conference on Mathematics of Operational Research, Aston - *Queueing networks, Deadlock and Healthcare*
* Feb 2017 - PyCon Namibia, Windhoek - *Producing Pretty Plots in Python*
* Sept 2016 - PyCon UK, Cardiff - *Queueing and Python: pip install ciw*
* May 2016 - CORS 2016, Banff - *Deadlock in Queueing Networks*
* May 2016 - Cynhadledd Wyddonol y CCC, Aberystwyth - Poster: *Llwyrglo yn Rhwydweithiau Ciwio* (Winner best poster)
* Mar 2016 - 8th IMA International Conference on Quantitative Modelling in the Management of Health and Social Care, London - *Using Queueing Networks Modelling to Assess the Impact of the OPICP*
* Jan 2016 - PyCon Namibia, Windhoek - *Simulating Queues with Ciw*
* Sept 2015 - Young OR 19, Aston - *Queueing Networks for a Healthcare System, Deadlocking & Reinforcement Learning*
* July 2015 - EURO 2015, Glasgow - *Queueing Networks for a Healthcare System Deadlocking, Reinforcement Learning & Workforce Planning*
* Feb 2015 - Python Namibia 2015, Windhoek - *Playing with Reinforcement Learning in Python*


## Media Appearances

* 06/11/2020 - **Yfory Newydd** - *BBC Radio Cymru*


## Contact

Email: palmergi1@cardiff.ac.uk

References available on request.