---
layout: page
title: Wiki
description: wiki
keywords: 维基, Wiki
comments: false
menu: wiki
permalink: /wiki/
---

> How many commands and shortcuts will make your head explode?

<ul class="listing">
{% for wiki in site.wiki %}
{% if wiki.title != "Wiki Template" %}
<li class="listing-item"><a href="{{ site.url }}{{ wiki.url }}">{{ wiki.title }}</a></li>
{% endif %}
{% endfor %}
</ul>
