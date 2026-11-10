---
layout: page
title: Tags
permalink: /tags/
---

<!-- 상단 태그 칩/배지 목록 -->
<div class="tag-cloud" style="margin-bottom: 2rem; line-height: 2;">
  {% capture site_tags %}{% for tag in site.tags %}{{ tag[0] }}{% unless forloop.last %},{% endunless %}{% endfor %}{% endcapture %}
  {% assign tag_words = site_tags | split:',' | sort %}
  {% for item in tag_words %}
    <a href="#{{ item | slugify }}" style="margin-right: 8px; padding: 2px 8px; background: #f0f0f0; border-radius: 4px; text-decoration: none; font-size: 0.9rem;">
      #{{ item }} ({{ site.tags[item].size }})
    </a>
  {% endfor %}
</div>

<hr>

<!-- 태그별 포스트 목록 -->
{% for item in tag_words %}
  <h3 id="{{ item | slugify }}">{{ item }}</h3>
  <ul>
    {% for post in site.tags[item] %}
      <li style="margin-bottom: 0.3rem;">
        <span style="color: #888; font-family: monospace; margin-right: 0.5rem;">
          {{ post.date | date: "%Y-%m-%d" }}
        </span>
        <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
      </li>
    {% endfor %}
  </ul>
{% endfor %}