---
layout: page
title: projects
permalink: /portfolio/
---
<!--
{% assign shuffled_portfolio = site.portfolio | shift | sample: 7 %}
-->
Some of the fun stuff I entertained myself with in my free time in the past :). To check what I do research on and which student projects I offer, go to <a href="{{ site.baseurl }}/research/" target="_blank">research</a> tab.

{% for project in site.portfolio %}

{% if project.title == "Martin for TU Delft iGEM Supervisor" %}
{% else %}

{% if project.redirect %}
<div class="project">
    <div class="thumbnail">
        <a href="{{ project.redirect }}" target="_blank">
        {% if project.img %}
        <img class="thumbnail" src="{{ project.img }}"/>
        {% else %}
        <div class="thumbnail blankbox"></div>
        {% endif %}
        <span>
            <h1>{{ project.title }}</h1>
            <br/>
            <p>{{ project.description }}</p>
        </span>
        </a>
    </div>
</div>
{% else %}

<div class="project ">
    <div class="thumbnail">
        <a href="{{ site.baseurl }}{{ project.url }}">
        {% if project.img %}
        <img class="thumbnail" src="{{ project.img }}"/>
        {% else %}
        <div class="thumbnail blankbox"></div>
        {% endif %}
        <span>
            <h1>{{ project.title }}</h1>
            <br/>
            <p>{{ project.description }}</p>
        </span>
        </a>
    </div>
</div>

{% endif %}
{% endif %}

{% endfor %}

<br/>
<hr/>
<br/>
