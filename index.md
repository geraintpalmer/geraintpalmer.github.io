---
layout: default
---

### About

 + Lecturer at Cardiff University.
 + Research interests: stochastic modelling, queueing theory, simulation, [Ciw](https://ciw.readthedocs.io/en/latest/).
 + Software development and teaching.
 + Bilingual: English, Cymraeg ![icon](/images/logo-cymraeg.png){: style="width: 14px"}.


### Publications

<ul>
{% for pub in site.data.publications %}
  {% if pub.journal == 'NA' %}
    <li>{{ pub.year }}: <b>{{ pub.title }}</b><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<i>{{ pub.authors }}</i> <a class="page-link" href="{{ pub.link }}">Under review, on arXiv.</a></li>
  {% else %}
    {% if pub.multilang == 'no' %}
    <li>{{ pub.year }}: <b>{{ pub.title }}</b><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<i>{{ pub.authors }}</i> <a class="page-link" href="{{ pub.link }}">{{ pub.journal }}</a>
    </li>
    {% elsif pub.lang == 'en'%}
    <li>{{ pub.year }}: <b>{{ pub.title }}</b> <a class="page-link" href="{{ pub.altlink }}">(cy)</a><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<i>{{ pub.authors }}</i> <a class="page-link" href="{{ pub.link }}">{{ pub.journal }}</a>
    </li>
    {% endif %}
  {% endif %}
{% endfor %}
</ul>

### Book

<ul>
{% for book in site.data.books %}
  <li>{{ book.year }}: <b>{{ book.title }}</b><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<i>{{ book.authors }}</i> <a class="page-link" href="{{ book.link }}">{{ book.publisher}}, ISBN: {{ book.isbn }}</a>
  </li>
{% endfor %}
</ul>


[Research Assets](/assets/) ⸰ [Institution Page](https://www.cardiff.ac.uk/people/view/1067369-palmer-geraint) ⸰ [Google Scholar](https://scholar.google.com/citations?hl=en&user=PYovOSUAAAAJ) ⸰ [ORCID](https://orcid.org/0000-0001-7865-6964) ⸰ [ResearchGate](https://www.researchgate.net/profile/Geraint-Palmer)
