---
layout: default
---

### About

 + PhD student at Cardiff University.
 + Welsh language teaching associate.
 + Software development and teaching.
 + Research interests: stochastic modelling, queueing theory, simulation.
 + Bilingual: English, Cymraeg.


### Publications

<ul>
{% for pub in site.data.publications %}
  <li><b>{{ pub.title }}</b> <i>{{ pub.authors }}</i> 
  	{% if pub.published == 'yes' %}
  	  <a class="page-link" href="{{ pub.link }}">{{ pub.journal }}</a>
  	{% else %}
  	  Under Review.
  	{% endif %}
  </li>
{% endfor %}
</ul>

[Research Assets](/assets/)
