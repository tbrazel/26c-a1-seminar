---
layout: page
title: Information
permalink: /information/
---

The seminar meets {{ site.seminar.meets | downcase }} in {{ site.seminar.room }}.
Talks are 50 minute, with questions after (and also hopefully during!)

## Speaking

Please email tbraz@alumni.upenn.edu if you'd like to speak!

## Keeping up

{% if site.seminar.mailing_list and site.seminar.mailing_list != '' %}Announcements go out on the [mailing list]({{ site.seminar.mailing_list }}) about a week before each talk.{% else %}Announcements go out on the mailing list about a week before each talk.{% endif %}
{% if site.seminar.calendar and site.seminar.calendar != '' %}The schedule is also published as a [calendar feed]({{ site.seminar.calendar }}) you can subscribe to.{% endif %}

## Organizers

{% for o in site.organizers %}
- {% if o.url and o.url != '' %}[{{ o.name }}]({{ o.url }}){% else %}{{ o.name }}{% endif %}{% if o.email and o.email != '' %}, [{{ o.email }}](mailto:{{ o.email }}){% endif %}
{%- endfor %}
