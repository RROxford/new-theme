---
title: "What's on"
tagline: "What's going on in Oxford?"
description: Events and initiatives
type: page
permalink: /events/
---
---

<p> <h2> Please note this webpage is no longer updated. Please go to the new
website at <a href="https://rr.ox.ac.uk/">https://rr.ox.ac.uk/</a> for the most
recent information.</h2> </p>

# Events

Below is a list of reproducibility-related events happening in or around Oxford. At the bottom of this page you'll also find some ongoing [initiatives](#initiatives), as well as a list of [past events](#pastEvents).
For each of our activities, please follow our [Code of Conduct]({{ site.url }}{{ site.baseurl }}/misc/RROxCoC.pdf){:target="_blank"} which relies on the [UKRN Code of Conduct](https://www.ukrn.org/code-of-conduct/){:target="_blank"}.

<div id="accordion">
{% assign events = site.events | sort: "expires" %}
{% for event in events %}
    {% include event_card event=event %}
{% endfor %}
</div>

# Initiatives

Here is a list of ongoing initiatives related to RROx.

<div id="accordion">
{% for event in site.initiatives %}
    {% include event_card event=event %}
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
    let expires = e.dataset.dateEnds;
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
      if(new Date(cards[i].dataset.dateEnds) < date)
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
    let year = new Date(cards[i].dataset.dateEnds).getFullYear();
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
