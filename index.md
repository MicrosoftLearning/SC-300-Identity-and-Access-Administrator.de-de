---
title: Online gehostete Anweisungen
permalink: index.html
layout: home
---

# Inhaltsverzeichnis

Erforderliche Dateien für Labs können [hier](https://github.com/MicrosoftLearning/SC-300-Identity-and-Access-Administrator/archive/master.zip) heruntergeladen werden.

Hyperlinks zu den Lab-Übungen und Demos sind nachfolgend aufgelistet.

## Labs

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| Modul | Lab |
| --- | --- | 
{% for activity in labs  %}| {{ activity.lab.module }} | [{{ activity.lab.title }}{% if activity.lab.type %} – {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
