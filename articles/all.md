---
    title: All Posts
    permalink: /articles/all/
---

<h1>{{ page.title }}</h1>

<div class="linkList">
  {% for category in site.categories %}
    <h2>{{ category[0] | capitalize }}</h2>
    <ul>
      {% for post in category[1] %}
        <li>
          <h3>
            <a href="{{post.url}}">
              {% if post.series %}{{ post.series }} &mdash; {% endif %}
              {{post.title | markdownify | strip_html }}
            </a> &mdash;
            {{ post.date | date: "%m/%d/%y" }}
          </h3>
          <p>
            {{ post.excerpt }}
          </p>
        </li>
      {% endfor %}
    </ul>
  {% endfor %}
</div>
