---
layout: page
title: Information
permalink: /information/
---

The seminar meets {{ site.seminar.meets | downcase }} in {{ site.seminar.room }}.
Talks are one hour, with questions during rather than after — this is a working
seminar and interruptions are the point.

## Speaking

We are always looking for speakers, including graduate students giving their
first talk. Write to one of the organizers with a title and a short abstract,
and say roughly when you are free. Visitors passing through are welcome to ask
for a slot on short notice; we usually keep one or two open each term.

Abstracts may contain TeX. Inline math such as $H^1(X, \mathcal{O}_X)$ works,
and so does a displayed equation, as long as it sits in a paragraph of its own:

$$\chi(X, \mathcal{F}) = \sum_i (-1)^i \dim H^i(X, \mathcal{F}).$$

## Keeping up

{% if site.seminar.mailing_list and site.seminar.mailing_list != '' %}Announcements go out on the [mailing list]({{ site.seminar.mailing_list }}) about a week before each talk.{% else %}Announcements go out on the mailing list about a week before each talk.{% endif %}
{% if site.seminar.calendar and site.seminar.calendar != '' %}The schedule is also published as a [calendar feed]({{ site.seminar.calendar }}) you can subscribe to.{% endif %}

## Organizers

{% for o in site.organizers %}
- {% if o.url and o.url != '' %}[{{ o.name }}]({{ o.url }}){% else %}{{ o.name }}{% endif %}{% if o.email and o.email != '' %}, [{{ o.email }}](mailto:{{ o.email }}){% endif %}
{%- endfor %}
