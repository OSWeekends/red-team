---
---
# Recursos

{% for categoria in site.data.recursos %}
  {% assign nombre = categoria[0] %}
  {% assign recursos = categoria[1] %}

  <h2>{{ nombre }}</h2>
  <ul>
    {% for recurso in recursos %}
      <li><a href="{{ recurso.url }}">{{ recurso.nombre }}</a></li>
    {% endfor %}
  </ul>
{% endfor %}
