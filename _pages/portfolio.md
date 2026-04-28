---
permalink: /portfolio/
title: Portfolio
layout: single
classes: wide
author_profile: true
---

<div class="portfolio-grid">
{% assign sorted = site.portfolio | sort: "date" | reverse %}
{% for item in sorted %}
<article class="portfolio-card">
  <div class="portfolio-card__content">
    <h2 class="portfolio-card__title">
      <a href="{{ item.url | relative_url }}">{{ item.title }}</a>
    </h2>
    <div class="portfolio-card__date">{{ item.date | date: "%B %Y" }}</div>
    {% if item.tags.size > 0 %}
    <div class="portfolio-card__tags">
      {% for tag in item.tags %}<span class="portfolio-tag">{{ tag }}</span>{% endfor %}
    </div>
    {% endif %}
    <div class="portfolio-card__description">{{ item.description }}</div>
    {% if item.media %}
    <div class="portfolio-card__media">
      {% for m in item.media %}
        {% if m.type == "video" %}
        <video controls preload="none"{% if m.poster %} poster="{{ m.poster | relative_url }}"{% endif %}>
          <source src="{{ m.src }}" type="video/mp4">
        </video>
        {% elsif m.type == "image" %}
        <img src="{{ m.src | relative_url }}" alt="{{ m.alt | default: item.title }}" loading="lazy">
        {% elsif m.type == "embed" %}
        {{ m.html }}
        {% elsif m.type == "link" %}
        <a href="{{ m.src }}" class="portfolio-card__file-link">{{ m.label | default: "View file" }}</a>
        {% endif %}
      {% endfor %}
    </div>
    {% endif %}
  </div>
</article>
{% endfor %}
</div>
