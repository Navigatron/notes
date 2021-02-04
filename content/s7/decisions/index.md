[Index](../../../index.md) > Decision Analysis

# PUBL 302: Decision Analysis

First class was syllabus review.

[2021-01-28: BCA](./2021-01-28.md)

[2021-02-02: Graphics and Estimation](./2021-02-02.md)

[2021-02-04: Reading Discussions](./2021.02-04.md)

## This is a test, this is only a test.

This list of sub-pages is automatically generated:

{% assign parenturl = page.url | remove:'/index.html' %}
{% for sibling in site.pages %}
{% if sibling.url contains parenturl %}
{% unless sibling.url == page.url %}
[{{ sibling.date }}: {{ sibling.title }}]({{ sibling.url | relative_url }})
{% endunless %}
{% endif %}
{% endfor %}
