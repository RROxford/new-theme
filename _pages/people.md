---
title: "People"
tagline: "Key people"
description: Key people
permalink: /people/
type: page
---
---

<p> <h2> Please note this webpage is no longer updated. Please go to the new
website at <a href="https://rr.ox.ac.uk/">https://rr.ox.ac.uk/</a> for the most
recent information.</h2> </p>

In line with its cross-disciplinary remit, RROx is represented by members from the four academic Divisions of the
University of Oxford. Group members span all career stages,
from DPhil student to senior professor.

Additionally, representation from the Bodleian Libraries provides
liaison with relevant units in Gardens, Libraries & Museums. Research Services are also represented.

[RROx Fellows](/all_groups#RROxFellows) are involved in RROx by leading on specific [initiatives]({{
"/all_groups" | relative_url }}).


<div class="initial-content person-card-columns" id="accordion">
  {% assign people = site.team | sort_natural: 'lastname' %}
  {% for person in people %}
    {% unless person.retired %}
        {% include person_card person=person %}
    {% endunless %}
  {% endfor %}

  {% for person in people %}
      {% if person.retired %}
          {% include person_card person=person %}
      {% endif %}
    {% endfor %}
</div>

{% assign groupArray = "a, b, c" | split: ", " %}
{% for person in site.team %}
  {% if forloop.first == true %}
    {% assign groupArray = person.groups %}
  {% else %}
    {% assign groupArray = groupArray | push: person.groups %}
  {% endif %}
{% endfor %}
{% assign groupArray = groupArray | uniq %}

{% for g in groupArray %}
  {% include group_list group=g %}
{% endfor %}


{% assign affArray = "a, b, c" | split: ", " %}
{% for person in site.team %}
  {% if forloop.first == true %}
    {% assign affArray = person.affiliations %}
  {% else %}
    {% assign affArray = affArray | push: person.affiliations %}
  {% endif %}
{% endfor %}
{% assign affArray = affArray | uniq %}

{% for a in affArray %}
  {% include affiliation_list affiliation=a %}
{% endfor %}

<script>
  setTimeout(function () {
    openCard();
  }, 100);

  document.body.addEventListener('click', function(e){closeCards(e)});
</script>


# Past members

<div class="initial-content person-card-columns" id="accordion">
  {% assign people = site.past_team | sort_natural: 'lastname' %}
  {% for person in people %}
    {% unless person.retired %}
        {% include person_card person=person %}
    {% endunless %}
  {% endfor %}

  {% for person in people %}
      {% if person.retired %}
          {% include person_card person=person %}
      {% endif %}
    {% endfor %}
</div>
