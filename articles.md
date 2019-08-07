---
    title: Articles
    permalink: /articles/
---

<!--![Article Pages](/assets/images/scientific-article-stack.png)-->

# Articles

Here are list of blog series that I write.
Most of them are here but there are a few stragglers.
You can view a reverse-chronological listing of all of my posts [here](/articles/all).

## Python for Math Majors

I write a series of python tutorials aimed at people coming from a math background.

<div class="linkList">
    <ul>
        {% assign count = '0' %}
        {% for post in site.posts reversed %}
            {% if post.series == "Python for the Math Major" %}
                {% capture count %}{{ count | plus: '1' }}{% endcapture %}
                <li>Part {{ count }} -
                    <a href="{{post.url}}">{{post.title | markdownify | strip_html }}</a>
                </li>
            {% endif %}
        {% endfor %}
    </ul>
</div>
