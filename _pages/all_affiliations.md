---

title: People listed by affiliation
type: page
permalink: /all_affiliations

---
---
{% comment %} Iterate through people and build a list of affiliations {% endcomment %}
{% assign affArray = "a, b, c" | split: ", " %}

{% for person in site.team %}

  {% if forloop.first == true %}
    {% assign affArray = person.affiliations %}
  {% else %}
    {% assign affArray = affArray | concat: person.affiliations %}
  {% endif %}
{% endfor %}
{% assign affArray = affArray | uniq %}
{% assign affArray = affArray | sort %}

{% comment %} List each affiliation and the people in it {% endcomment %}

{% for affiliation in affArray %}
  <div class="card affiliation-list">
    <div class="card-header show" data-toggle="collapse" data-target="#{{ affiliation }}" tabindex="0" onkeydown="clickMe(event)">{{ affiliation }}</div>
    <div class="card-body collapse" id="{{ affiliation | replace: " ", "" }}">
      {% for person in site.team %}
        {% if person.affiliations contains affiliation %}
          <button type="button" class="btn btn-block" onclick="window.location.assign('{{ '/' | relative_url }}people/#{{- person.firstname | append: person.lastname | replace: " ", "" -}}')" tabindex="0" onkeydown="clickMe(event)">
            {{ person.firstname }} {{ person.lastname}}
          </button>
        {% endif %}
      {% endfor %}
    </div>
  </div>
{% endfor %}
