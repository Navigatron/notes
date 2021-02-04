[Index](../../../index.md) > Decision Analysis

# PUBL 302: Decision Analysis

> This page auto-generates its index of subpages. Things may break. This is experimental.

First class was syllabus review.

{% assign parenturl = page.url | remove:'/index.html' %}
{% for sibling in site.pages %}
{% if sibling.url contains parenturl %}
{% unless sibling.url == page.url %}
[{{ sibling.date }}: {{ sibling.title }}]({{ sibling.url | relative_url }})
{% endunless %}
{% endif %}
{% endfor %}
