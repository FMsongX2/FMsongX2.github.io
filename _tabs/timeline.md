---
title: 이력
icon: fas fa-trophy
order: 0
---

{% assign kinds = "award:수상,finalist:Finalist,activity:활동,opensource:오픈소스" | split: "," %}

<a class="boj-badge" href="https://solved.ac/profile/songsong97" target="_blank" rel="noopener"><img src="https://mazassumnida.wtf/api/v2/generate_badge?boj=songsong97" alt="백준 songsong97 solved.ac 티어 배지" width="350" height="170"></a>

<div class="timeline">
{% assign groups = site.data.timeline | group_by_exp: "item", "item.date | slice: 0, 4" %}
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
        <span class="timeline-title">{{ item.title }}</span>
        {% if item.org %}<span class="timeline-org">{{ item.org }}</span>{% endif %}
      </div>
    </li>
  {% endfor %}
  </ul>
{% endfor %}
</div>
