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
  {% if pub.multilang == 'no' %}
  <li>{{ pub.year }}: <b>{{ pub.title }}</b><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<i>{{ pub.authors }}</i> <a class="page-link" href="{{ pub.link }}">{{ pub.journal }}</a>
  </li>
  {% elsif pub.lang == 'en'%}
  <li>{{ pub.year }}: <b>{{ pub.title }}</b> <a class="page-link" href="{{ pub.altlink }}">(cy)</a><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<i>{{ pub.authors }}</i> <a class="page-link" href="{{ pub.link }}">{{ pub.journal }}</a>
  </li>
  {% endif %}
{% endfor %}
</ul>

[Research Assets](/assets/) ⸰ [Google Scholar](https://scholar.google.com/citations?hl=en&user=PYovOSUAAAAJ)
