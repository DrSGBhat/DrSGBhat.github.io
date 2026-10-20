---
layout: archive
title: "Sitemap"
description: "Every page and publication on Sandesh G. Bhat's website."
permalink: /sitemap/
author_profile: true
---

{% include base_path %}

{% comment %}
  Lists the site's pages and publications. Pages with `sitemap: false` in
  their front matter (404, Awards, Travel, Photography) and files without a
  title (stylesheets, feeds, redirects, robots.txt) are left out, the same
  pages that sitemap.xml leaves out.
{% endcomment %}
{% assign visible = site.pages | where_exp: "p", "p.title" | where_exp: "p", "p.sitemap != false" | where_exp: "p", "p.url != page.url" %}

All the pages on this site. Search engines can use the [XML sitemap]({{ base_path }}/sitemap.xml).

<h2>Pages</h2>
<ul>
  {% assign home = visible | where: "url", "/" | first %}
  {% if home %}<li><a href="{{ base_path }}/">Home</a></li>{% endif %}
  {% for item in site.data.navigation.main %}
    {% assign p = visible | where: "url", item.url | first %}
    {% if p %}<li><a href="{{ base_path }}{{ p.url }}">{{ item.title }}</a></li>{% endif %}
  {% endfor %}
  {% for p in visible %}
    {% assign in_menu = site.data.navigation.main | where: "url", p.url | first %}
    {% unless in_menu or p.url == "/" %}<li><a href="{{ base_path }}{{ p.url }}">{{ p.title }}</a></li>{% endunless %}
  {% endfor %}
</ul>

<h2>Publications</h2>
{% assign pubs = site.publications | sort: "date" | reverse %}
<ul>
  {% for p in pubs %}
    <li><a href="{{ base_path }}{{ p.url }}">{{ p.title }}</a> ({{ p.date | date: "%Y" }})</li>
  {% endfor %}
</ul>
