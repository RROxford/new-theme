---
title: "People"
tagline: "Find your key contacts"
description: Key people involved in ReproducibleResearchOxford
permalink: /people/
type: page
---

---
RROx is run by a Steering Group and several others who lead on
specific [initiatives]({{ "/all_groups" | relative_url }}).

You can also see who is involved by [affiliation]({{
"/all_affiliations" | relative_url }}).

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
    {% assign groupArray = groupArray | concat: person.groups %}
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
    {% assign affArray = affArray | concat: person.affiliations %}
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
