---
layout: page
title: Reading
subtitle: Books that have stayed with me
permalink: /reading/
---

{% assign r = site.data.reading %}

{% if r.recent.size > 0 %}
## Currently reading
{% include book_list.html books=r.recent %}
{% endif %}

## All-time favorites
{% include book_list.html books=r.favorites %}
