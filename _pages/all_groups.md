---

title: Ambassadors listed by group
type: page
permalink: /all_groups

---
---
{% comment %} Iterate through people and build a list of groups {% endcomment %}
{% assign groupArray = "a, b, c" | split: ", " %}

{% for person in site.team %}

  {% if forloop.first == true %}
    {% assign groupArray = person.groups %}
  {% else %}
    {% assign groupArray = groupArray | push: person.groups %}
  {% endif %}
{% endfor %}
{% assign groupArray = groupArray | uniq %}

{% comment %} List each group and the people in it {% endcomment %}

{% for group in groupArray %}
  <div class="card group-list">
    <div class="card-header" data-toggle="collapse" data-target="#{{ group }}" tabindex="0" onkeydown="clickMe(event)">
      <a href="{{ '/' | relative_url }}initiatives/#{{- group | replace: " ", "" -}}">{{ group }}</a>
      <div class="close"><i class="fas fa-angle-double-down"></i></div>
    </div>
    <div class="card-body collapse" id="{{ group }}">
      {% for person in site.team %}
        {% if person.groups contains group %}
          <button type="button" class="btn btn-block" onclick="window.location.assign('{{ '/' | relative_url }}people/#{{- person.firstname | append: person.lastname | replace: " ", "" -}}')" tabindex="0" onkeydown="clickMe(event)">
            {{ person.firstname }} {{ person.lastname}}
          </button>
        {% endif %}
      {% endfor %}
    </div>
  </div>
{% endfor %}
