---
layout: default
title: Blog
hero_description: Technical writing on Red Team, malware, threat intelligence, security reviews, risk, and adversarial thinking.
---

<div class="blog-language-view" data-blog-language>
  <div class="blog-language-toolbar">
    <span>View posts in:</span>

    <div class="blog-language-switch" role="tablist" aria-label="Blog language">
      <button type="button" data-language-button="en" aria-selected="true">
        English
      </button>

      <button type="button" data-language-button="es" aria-selected="false">
        Spanish
      </button>
    </div>
  </div>

  <section class="blog-language-panel" data-language-panel="en">
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

  <section class="blog-language-panel" data-language-panel="es" hidden>
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
</div>

<script>
  (() => {
    const root = document.querySelector("[data-blog-language]");
    if (!root) return;

    const buttons = root.querySelectorAll("[data-language-button]");
    const panels = root.querySelectorAll("[data-language-panel]");
    const storageKey = "blog-language";
    const savedLanguage = localStorage.getItem(storageKey);
    const browserLanguage = navigator.language.toLowerCase().startsWith("es") ? "es" : "en";
    const initialLanguage = savedLanguage || browserLanguage;

    function setLanguage(language) {
      buttons.forEach((button) => {
        const active = button.dataset.languageButton === language;
        button.setAttribute("aria-selected", active ? "true" : "false");
      });

      panels.forEach((panel) => {
        panel.hidden = panel.dataset.languagePanel !== language;
      });

      localStorage.setItem(storageKey, language);
    }

    buttons.forEach((button) => {
      button.addEventListener("click", () => {
        setLanguage(button.dataset.languageButton);
      });
    });

    setLanguage(initialLanguage);
  })();
</script>
