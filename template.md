---
layout: page
title: Template Language
nav_order: 2
---

# Template Language

HotStone using [go template](https://golang.org/pkg/text/template/) as its template engine

## Some illustration

![Data Sourcing](assets/images/data-sourcing.png)
{: .prop}


Given a data (from API): 
```json
{
   "name": "Ngurah Rai International Airport",
   "city": "Denpasar",
   "country": "Indonesia",
}
```

With template (stored in Hotstone):
{% raw %}
```html
<meta name="description" content="{{.Name}} adalah bandara di kota {{.City}} - {{.Country}}"/>
```
{% endraw %}

The result will be (render to frontend):
```html
<meta name="description" content="Ngurah Rai International Airport adalah bandara di kota Denpasar - Indonesia"/>
```


_TODO: Template Use Cases_


