---
layout: page
title: Preparing Template
parent: User Guides
nav_order: 3
---

{% raw %}

# Preparing Template

Hot-Stone using [handlebars](http://handlebarsjs.com/) as its template engine for 


## Simple Expressions

Data:
```json
{
  "firstname": "Yehuda",
  "lastname": "Katz"
}
```

Template:
```html
<p>{{firstname}} {{lastname}}</p>
```


## Nested Input Objects

Data:
```json
{
  "person": {
    "firstname": "Yehuda",
    "lastname": "Katz"
  }
}
```

Template:
```html
<p>{{person.firstname}} {{person.lastname}}</p>
```

## HTML Escaping

It's handle HTML Escaping by default. If you don't want Handlebars to escape a value, use the "triple-stash", `{{{`:

Data:
```json
{ "specialChars": "& < > \" ' ` =" }
```

Template:
```
raw: {{{specialChars}}}
html-escaped: {{specialChars}}
```


## Iterate List

Data:
```json
{
  "people": [
    "Yehuda Katz",
    "Alan Johnson",
    "Charles Jolley"
  ]
}
```

Template:
```html
<ul class="people_list">
  {{#each people}}
    <li>{{this}}</li>
  {{/each}}
</ul>
```

## Condition

Template:
```html
{{#if isActive}}
  <img src="star.gif" alt="Active">
{{else}}
  <img src="cry.gif" alt="Inactive">
{{/if}}
```


{% endraw %}