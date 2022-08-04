[Index](../../../index.md) > Cyber Risk and Resilience

# MGIS 429: Cyber: Risk and Resilience

> 2022 - changing rendering engines, will re-work this eventually.

{% raw %}
{% assign parenturl = page.url | remove:'/index.html' %}
{% for sibling in site.pages %}
{% if sibling.url contains parenturl %}
{% unless sibling.url == page.url %}
[{{ sibling.date }}: {{ sibling.title }}]({{ sibling.url | relative_url }})
{% endunless %}
{% endif %}
{% endfor %}
{% endraw %}