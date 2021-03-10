---
layout: default
---

### About

 + Lecturer at Cardiff University.
 + Research interests: stochastic modelling, queueing theory, simulation.
 + Software development and teaching.
 + Bilingual: English, Cymraeg.


### Publications

<ul>
{% for pub in site.data.publications %}
  <li>{{ pub.year }}: <b>{{ pub.title }}</b><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<i>{{ pub.authors }}</i> 
  	{% if pub.published == 'yes' %}
  	  <a class="page-link" href="{{ pub.link }}">{{ pub.journal }}</a>
  	{% elsif pub.preprint == 'yes' %}
  	  Under Review. <a class="page-link" href="{{ pub.link }}">{{ pub.arxiv }}</a>
  	{% else %}
  	  Under Review.
  	{% endif %}
  </li>
{% endfor %}
</ul>

[Research Assets](/assets/)
