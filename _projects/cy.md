---
layout: default
permalink: projects/cy/
---

# Prosiectau

Prosiectau presennol a gorffenol. ([In English](/projects/))

### Presennol

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