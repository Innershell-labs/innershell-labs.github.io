---
layout: default
title: Blog
hero_description: Technical writing on Red Team, malware, threat intelligence, security reviews, risk, and adversarial thinking.
---

<div class="blog-language-grid">
  <section class="blog-column">
    <div class="blog-column-header">
      <span>ES</span>
      <h2>Publicaciones en español</h2>
    </div>

    <ol class="blog-post-list">
      {% assign spanish_posts = site.posts | where: "lang", "es" %}
      {% for post in spanish_posts %}
        <li>
          <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
          <time datetime="{{ post.date | date_to_xmlschema }}">
            {{ post.date | date: "%Y-%m-%d" }}
          </time>
        </li>
      {% endfor %}
    </ol>
  </section>

  <section class="blog-column">
    <div class="blog-column-header">
      <span>EN</span>
      <h2>Posts in English</h2>
    </div>

    <ol class="blog-post-list">
      {% assign english_posts = site.posts | where: "lang", "en" %}
      {% for post in english_posts %}
        <li>
          <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
          <time datetime="{{ post.date | date_to_xmlschema }}">
            {{ post.date | date: "%Y-%m-%d" }}
          </time>
        </li>
      {% endfor %}
    </ol>
  </section>
</div>
