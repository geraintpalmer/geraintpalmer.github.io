---
layout: default
title: Projects
---

# Projects

Current and past projects. ([Yn Gymraeg](/projects/cy/))

{% assign show = false %}
{% for proj in site.data.proj %}
  {% if proj.current == 'yes' %}
    {% assign show = true %}
  {% endif %}
{% endfor %}

{% if show == true %}

<h3>Current</h3>

<ul>
{% for proj in site.data.proj %}
  {% if proj.current == 'yes' %}
  <li>{{ proj.year }}: <b>{{ proj.title }}</b><br>
  <ul>
  {% if proj.amount != 'na' %}
  <li><i>{{ proj.amount }}</i> - {{ proj.fundingbody }}</li>
  {% endif %}
  {% if proj.role != 'na' and proj.with != 'na' %}
  <li><b>{{ proj.role }}</b> with {{ proj.with }}</li>
  {% elsif proj.role == 'na' and proj.with != 'na' %}
  <li>With {{ proj.with }}</li>
  {% endif %}
  <li>{{ proj.summary }}</li>
  </ul>
  </li><br>
  {% endif %}
{% endfor %}
</ul>

{% endif %}

### Past

<ul>
{% for proj in site.data.proj %}
  {% if proj.current == 'no' %}
  <li>{{ proj.year }}: <b>{{ proj.title }}</b><br>
  <ul>
  {% if proj.amount != 'na' %}
  <li><i>{{ proj.amount }}</i> - {{ proj.fundingbody }}</li>
  {% endif %}
  {% if proj.role != 'na' and proj.with != 'na' %}
  <li><b>{{ proj.role }}</b> with {{ proj.with }}</li>
  {% elsif proj.role == 'na' and proj.with != 'na' %}
  <li>With {{ proj.with }}</li>
  {% endif %}
  <li>{{ proj.summary }}</li>
  </ul>
  </li><br>
  {% endif %}
{% endfor %}
</ul>