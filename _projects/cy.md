---
layout: default
title: Prosiectau
permalink: projects/cy/
---

# Prosiectau

<div style="text-align: right; font-size: large;">
  <a href="/projects/">Fersiwn Saesneg <img class="emoji" draggable="false" src="https://twemoji.maxcdn.com/2/svg/1f1ec-1f1e7.svg"/></a>
</div>

Prosiectau presennol a gorffenol.

{% assign show = false %}
{% for proj in site.data.proj %}
  {% if proj.current == 'yes' %}
    {% assign show = true %}
  {% endif %}
{% endfor %}

{% if show == true %}

<h3>Presennol</h3>

<ul>
{% for proj in site.data.proj %}
  {% if proj.current == 'yes' %}
  <li>{{ proj.year }}: <b>{{ proj.teitl }}</b><br>
  <ul>
  {% if proj.amount != 'na' %}
  <li><i>{{ proj.amount }}</i> - {{ proj.corffcyllido }}</li>
  {% endif %}
  {% if proj.rol != 'na' and proj.gyda != 'na' %}
  <li><b>{{ proj.rol }}</b> gyda {{ proj.gyda }}</li>
  {% elsif proj.rol == 'na' and proj.gyda != 'na' %}
  <li>Gyda {{ proj.gyda }}</li>
  {% endif %}
  <li>{{ proj.crynodeb }}</li>
  </ul>
  </li><br>
  {% endif %}
{% endfor %}
</ul>

{% endif %}

### Gorffenol

<ul>
{% for proj in site.data.proj %}
  {% if proj.current == 'no' %}
  <li>{{ proj.year }}: <b>{{ proj.teitl }}</b><br>
  <ul>
  {% if proj.amount != 'na' %}
  <li><i>{{ proj.amount }}</i> - {{ proj.corffcyllido }}</li>
  {% endif %}
  {% if proj.rol != 'na' and proj.gyda != 'na' %}
  <li><b>{{ proj.rol }}</b> gyda {{ proj.gyda }}</li>
  {% elsif proj.rol == 'na' and proj.gyda != 'na' %}
  <li>Gyda {{ proj.gyda }}</li>
  {% endif %}
  <li>{{ proj.crynodeb }}</li>
  </ul>
  </li><br>
  {% endif %}
{% endfor %}
</ul>