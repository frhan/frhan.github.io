---
layout: page
title: About
description: 打码改变世界
keywords: Farhan,Faruque
comments: true
menu: About
permalink: /about/
---
## Farhan Faruque..Full stack Software Engineer

## Contact

{% for website in site.data.social %}
* {{ website.sitename }}：[@{{ website.name }}]({{ website.url }})
{% endfor %}

## Skill Keywords

{% for category in site.data.skills %}
### {{ category.name }}
<div class="btn-inline">
{% for keyword in category.keywords %}
<button class="btn btn-outline" type="button">{{ keyword }}</button>
{% endfor %}
</div>
{% endfor %}
