---
title: "Publications"
description: "Journal articles, conference papers, and theses by Sandesh G. Bhat on upper extremity orthoses, brachial plexus injury, gait dynamics, and rehabilitation robotics."
permalink: /publications/
author_profile: true
---

{% include base_path %}

For proper citations, refer to [Google Scholar](https://scholar.google.com/citations?user=Dx9aVjgAAAAJ&hl=en).<br>
updated: 10/19/2026

{% comment %} Entries live in _data/publications.yml {% endcomment %}
{% assign pubs = site.data.publications %}
{% assign number = pubs | size %}
{% assign years = pubs | group_by: "year" %}
{% for year in years %}
## {{ year.name }}

<ol class="publication-list" reversed start="{{ number }}">
{%- for pub in year.items %}
  {%- if pub.page %}{% capture link %}{{ base_path }}{{ pub.page }}{% endcapture %}
  {%- elsif pub.doi %}{% capture link %}https://doi.org/{{ pub.doi }}{% endcapture %}
  {%- else %}{% assign link = pub.url %}{% endif %}
  <li>
    <b>{% if link %}<a href="{{ link }}">{{ pub.title | escape }}</a>{% else %}{{ pub.title | escape }}{% endif %}</b><br>
    {{ pub.authors }}.<br>
    <i>{{ pub.journal | escape }}</i>.{% if pub.event %} <b>{{ pub.event | escape }}</b>.{% endif %}{% if pub.status %} {{ pub.status | escape }}.{% endif %}{% if pub.doi %} <a href="https://doi.org/{{ pub.doi }}">doi:{{ pub.doi }}</a>{% endif %}
  </li>
{%- endfor %}
</ol>
{% assign number = number | minus: year.size %}
{% endfor %}
