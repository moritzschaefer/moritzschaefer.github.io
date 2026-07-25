---
permalink: /portfolio/
title: Portfolio
layout: single
classes:
  - wide
  - portfolio-page
author_profile: false
---

<p class="portfolio-intro">Non-reviewed artifacts from my life as a scientist.</p>

<div class="portfolio-grid">
{% assign sorted = site.portfolio | sort: "date" | reverse %}
{% for item in sorted %}
<article class="portfolio-card">
  <div class="portfolio-card__content">
    <div class="portfolio-card__head">
      <h2 class="portfolio-card__title"><a href="{{ item.url | relative_url }}">{{ item.title }}</a></h2>
      <time class="portfolio-card__date">{{ item.date | date: "%B %Y" }}</time>
    </div>
    {% if item.tags.size > 0 %}
    <div class="portfolio-card__tags">
      {% for tag in item.tags %}<span class="portfolio-tag">{{ tag }}</span>{% endfor %}
    </div>
    {% endif %}
    {% if item.description %}<p class="portfolio-card__description">{{ item.description }}</p>{% endif %}
  </div>
  {% if item.media %}
  <div class="portfolio-card__media">
    {% include portfolio-media.html media=item.media title=item.title limit=1 %}
  </div>
  {% endif %}
  <div class="portfolio-card__foot">
    <a class="portfolio-card__more" href="{{ item.url | relative_url }}">View project
      {% assign extra = item.media | size | minus: 1 %}
      {% if extra > 0 %}<span class="portfolio-card__count">+{{ extra }} more</span>{% endif %}
      <span aria-hidden="true">→</span>
    </a>
  </div>
</article>
{% endfor %}
</div>

{% include portfolio-scripts.html %}
