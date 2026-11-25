---
title: 이력
icon: fas fa-trophy
order: 4
---

{% assign kinds = "award:수상,finalist:Finalist,activity:활동,opensource:오픈소스,algorithm:알고리즘" | split: "," %}
{% assign featured = site.data.timeline | where: "featured", true %}
{% assign rest = site.data.timeline | where_exp: "item", "item.featured != true" %}

<div class="featured-awards">
{% for item in featured %}
  <div class="featured-card">
    <span class="featured-date">{{ item.date | replace: "-", "." }}</span>
    <span class="featured-title">{{ item.title }}</span>
    <span class="featured-org">{{ item.org }}</span>
    <div class="featured-foot">
      {% if item.prize %}<span class="featured-prize">상금 {{ item.prize }}</span>{% endif %}
      {% if item.post %}<a class="featured-post" href="{{ item.post | relative_url }}">수상소감 →</a>{% endif %}
    </div>
  </div>
{% endfor %}
</div>

<a class="boj-badge" href="https://solved.ac/profile/songsong97" target="_blank" rel="noopener"><img src="https://mazassumnida.wtf/api/v2/generate_badge?boj=songsong97" alt="백준 songsong97 solved.ac 티어 배지" width="350" height="170"></a>

<div class="timeline">
{% assign groups = rest | group_by_exp: "item", "item.date | slice: 0, 4" %}
{% for group in groups %}
  <h2 class="timeline-year">{{ group.name }}</h2>
  <ul class="timeline-list list-unstyled">
  {% for item in group.items %}
    {% assign kind_label = item.kind %}
    {% for pair in kinds %}
      {% assign kv = pair | split: ":" %}
      {% if kv[0] == item.kind %}{% assign kind_label = kv[1] %}{% endif %}
    {% endfor %}
    <li class="timeline-item">
      <span class="timeline-date">{{ item.date | replace: "-", "." }}{% if item.end %} – {{ item.end | replace: "-", "." }}{% endif %}</span>
      <div class="timeline-body">
        <span class="timeline-kind kind-{{ item.kind }}">{{ kind_label }}</span>
        {% if item.post %}<a class="timeline-title" href="{{ item.post | relative_url }}">{{ item.title }}</a>{% else %}<span class="timeline-title">{{ item.title }}</span>{% endif %}
        {% if item.org %}<span class="timeline-org">{{ item.org }}</span>{% endif %}
      </div>
    </li>
  {% endfor %}
  </ul>
{% endfor %}
</div>
