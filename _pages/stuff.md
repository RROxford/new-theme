---
title: "What's On"
tagline: "What's going on in Oxford?"
description: Key reproducibility initiatives in Oxford
type: page
permalink: /stuff/
---
---

# Events

Below is a list of reproducibility-related events happening in or around Oxford. At the bottom of this page you'll also find some ongoing [initiatives](#initiatives), as well as a list of [past events](#pastEvents).

<div id="accordion">
{% for event in site.events %}
  <div class="card event" data-expires-after='{{ event.expires | convert: "date" | date: "%Y-%m-%d" }}'>
    <div class="card-header" data-toggle="collapse" data-target="#{{- event.title | replace: " ", "" -}}" tabindex="0" onkeydown="clickMe(event)">
      {% if event.image_src %}
        <div class="logo">
          <img src="{{ 'assets/images/initiatives' | relative_url}}/{{ event.image_src }}"/>
        </div>
      {% endif %}
      <div class="brief">
        <p class="text-muted">{{ event.type }}</p>
        <h4>{{ event.title }}</h4>
      </div>
    </div>
    <div class="card-body collapse" id="{{- event.title | replace: " ", "" -}}" data-parent="#accordion">
      <div class="card-links">
        <ul class="border-left border-muted">
        {% if event.website %}
          <li><i class="fa fa-globe" aria-hidden="true"></i><a href="{{ event.website }}">Event website</a></li>
        {% endif %}
        {% if event.twitter %}
          <li><i class="fab fa-fw fa-twitter-square" aria-hidden="true"></i><a href="https://twitter.com/{{ event.twitter }}">@{{ event.twitter }}</a></li>
        {% endif %}
        {% if event.soundcloud %}
          <li><i class="fab fa-soundcloud"></i><a href="https://soundcloud.com/{{ event.soundcloud }}">Soundcloud</a></li>
        {% endif %}
        </ul>
      </div>
      <div class="event-detail">
        {{ event.content | markdownify }}
      </div>
      <div class="event-people">
        {% assign people = site.team | sort_natural: 'lastname' %}
        {% for person in people %}
          {% if person.groups contains event.title %}
            <div class="btn btn-outline-info" onclick="window.location.assign('{{ '/people' | relative_url }}#{{- person.firstname | append: person.lastname | replace: ' ', '' -}}')" tabindex="0" onkeydown="clickMe(event)">
              {{ person.firstname }} {{ person.lastname }}
            </div>
          {% endif %}
        {% endfor %}
      </div>
    </div>
  </div>
{% endfor %}
</div>

# Initiatives

Here is a list of ongoing initiatives related to RROx.

<div id="accordion">
{% for event in site.initiatives %}
  <div class="card event" data-expires-after='{{ event.expires | convert: "date" | date: "%Y-%m-%d" }}'>
    <div class="card-header" data-toggle="collapse" data-target="#{{- event.title | replace: " ", "" -}}" tabindex="0" onkeydown="clickMe(event)">
      {% if event.image_src %}
        <div class="logo">
          <img src="{{ 'assets/images/initiatives' | relative_url}}/{{ event.image_src }}"/>
        </div>
      {% endif %}
      <div class="brief">
        <p class="text-muted">{{ event.type }}</p>
        <h4>{{ event.title }}</h4>
      </div>
    </div>
    <div class="card-body collapse" id="{{- event.title | replace: " ", "" -}}" data-parent="#accordion">
      <div class="card-links">
        <ul class="border-left border-muted">
        {% if event.website %}
          <li><i class="fa fa-globe" aria-hidden="true"></i><a href="{{ event.website }}">Event website</a></li>
        {% endif %}
        {% if event.twitter %}
          <li><i class="fab fa-fw fa-twitter-square" aria-hidden="true"></i><a href="https://twitter.com/{{ event.twitter }}">@{{ event.twitter }}</a></li>
        {% endif %}
        {% if event.soundcloud %}
          <li><i class="fab fa-soundcloud"></i><a href="https://soundcloud.com/{{ event.soundcloud }}">Soundcloud</a></li>
        {% endif %}
        </ul>
      </div>
      <div class="event-detail">
        {{ event.content | markdownify }}
      </div>
      <div class="event-people">
        {% assign people = site.team | sort_natural: 'lastname' %}
        {% for person in people %}
          {% if person.groups contains event.title %}
            <div class="btn btn-outline-info" onclick="window.location.assign('{{ '/people' | relative_url }}#{{- person.firstname | append: person.lastname | replace: ' ', '' -}}')" tabindex="0" onkeydown="clickMe(event)">
              {{ person.firstname }} {{ person.lastname }}
            </div>
          {% endif %}
        {% endfor %}
      </div>
    </div>
  </div>
{% endfor %}
</div>

<h2 id="pastEvents">Past events</h2>
<div class="initial-content" id="accordionPast">

</div>

<h2>Historic events</h2>
<p>Other past events can be found on the archive of <a href="https://rroxford.github.io/events/">this website</a>.</p>


<script type="text/javascript">
  /* Move expired events into the Past Events section */
  // Get a list of expired cards sorted by most recent date
  let cards = [];
  document.querySelectorAll('#accordion > div').forEach((e)=> {
    let expires = e.dataset.expiresAfter;
    // Only count initiaitves with an expiry date
    if(expires.length === 0)
      return;
    let date;
    // Only count well-formatted dates
    try {
      date = new Date(expires);
    }
    catch(e) {
      return;
    }
    // And don't count dates in the future!
    if(date > new Date())
      return;
    // Insert into cards array in descending order
    let i = 0;
    while(i < cards.length) {
      if(new Date(cards[i].dataset.expiresAfter) < date)
        break;
      else
        i++;
    }
    cards.splice(i, 0, e);
  });

  // Don't show the past events heading if no past events to show
  if(cards.length === 0) {
    document.querySelector('#pastEvents').classList.add('hidden');
    document.querySelector('#accordionPast').classList.add('hidden');
  }

  // Create a new heading for each year, place the year's events therein, and
  // move it all into the accordionPast div.
  let currentYear = Infinity;
  let pastDiv = document.querySelector('#accordionPast');
  for(let i = 0; i < cards.length; i++) {
    let year = new Date(cards[i].dataset.expiresAfter).getFullYear();
    // New year heading
    if(year < currentYear) {
      pastDiv.appendChild(document.createElement('h3')).innerText = year;
      currentYear = year;
    }
    pastDiv.appendChild(cards[i]);
  }

  // Set new accordion parent
  document.querySelectorAll('#accordionPast div[data-parent="#accordion"]')
    .forEach((e)=>{
      e.dataset.parent = '#accordionPast';
    })

</script>

{% include scrollToId.html %}
