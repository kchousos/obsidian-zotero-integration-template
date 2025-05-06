---
title: "{{title}}"
authors: 
{%- for creator in creators %}
  - "[[{{creator.firstName}} {{creator.lastName}}]]"
{%- endfor %}
date: '{{ date | format("YYYY-MM-DD") }}'
created: {{ importDate | format("Y-MM-DD") }}
aliases:
  - '{{ importDate | format("YYYYMMDDHHmmss") }}'
key: "@{{citekey}}"
DOI: "{{DOI}}"
ISBN: "{{ISBN}}"
URL: "{{url}}"
tags:
  - resource/document
---
> [!cite] 
> 
> {{bibliography}}

{% if abstractNote -%}
> [!abstract]-
> 
> {{abstractNote -}}
{% endif %}

# Notes
{% persist "notes" %}

{% endpersist %}

# Annotations

{%- for annotation in annotations -%}
{%- if annotation.annotatedText and 'Gray' in annotation.colorCategory %}

## {{annotation.annotatedText | escape }}

{%- endif -%}
{%- if annotation.type == "image" %}

![[{{annotation.imageBaseName}}|{{annotation.comment}} (p. {{annotation.page or 1}})]]
{%- endif -%}
{%- if annotation.type == "note" %}

> [!note] 
> 
> {{annotation.comment}}, (p. {{annotation.page or 1}})
{%- endif -%}
{%- if annotation.annotatedText %}
{%- if annotation.colorCategory == "Yellow" and annotation.type == "highlight" %}

{{annotation.annotatedText}} (p. {{annotation.page or 1}})
{%- if annotation.comment %}

> {{annotation.comment}}
{%- endif %}
{%- endif -%}
{%- endif -%}
{%- endfor -%}