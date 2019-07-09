---
title: "People"
tagline: "Find your key contacts"
description: Key people involved in ReproducibleResearchOxford
permalink: /people/
type: page
---
---
Below you can find information on many people involved in reproducible research at Oxford. Click on a person to see more detailed information about them.

You can also find people by [project group]({{ "/all_groups" | relative_url }}) or [affiliation]({{ "/all_affiliations" | relative_url }}).

<div class="initial-content person-card-columns" id="accordion">
  {% assign people = site.team | sort_natural: 'lastname' %}
  
  {% for person in people %}
    {% if person.retired %}
        {% assign peopleRtd = peopleRtd | concat: person | concat: "," %}
    {% else %}
        {% assign peopleCur = peopleCur | concat: person | concat: "," %}
    {% endif %}
  {% endfor %}
  
  {% for person in peopleCur %}
    {% include person_card person=person %}
  {% endfor %}
  {% for person in peopleRtd %}
    {% include person_card person=person %}
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
