---
layout: page
title: outreach
permalink: /outreach/
---

I regularly challenge my creativity by picking up odd artsy projects. I have screen-printed some t-shirts and tote bags, drawn posters and wrote some verses in the past. At the moment I am still doing it purely for its own sake, but I am curious in exploring ways how to use these artistic vents to communicate science and synthetic biology to people who are outside of it! In the meantime check some of my blog posts at [tag-science](../tag/phd) and [tag-science](../tag/SynBio), check lightweight description of some computational and hardware projects I played with in the past below or get in touch if you would like to do a colab!

<!---
For now can check the [projects](../portfolio/) tab for some lightweight description of some computational and hardware projects I played with in the past!
--->

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
