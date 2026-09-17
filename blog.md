---
layout: default
title: Blog
page_kind: blog
hero_description: Technical writing on Red Team, malware, threat intelligence, security reviews, risk, and adversarial thinking.
---

<div data-blog-language>
  <div class="blog-control-band">
    <div class="site-shell">
      <div class="blog-language-toolbar">
        <span>View posts in</span>
        <div class="blog-language-switch" role="group" aria-label="Blog language">
          <button type="button" data-language-button="en" aria-pressed="true">English</button>
          <button type="button" data-language-button="es" aria-pressed="false">Español</button>
        </div>
      </div>
    </div>
  </div>

  <div class="blog-posts-band">
    <div class="site-shell">
      <section class="blog-language-panel" data-language-panel="en" aria-label="English posts">
        <ol class="blog-post-list">
          {% assign english_posts = site.posts | where: "lang", "en" %}
          {% for post in english_posts %}
            <li>
              <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%Y-%m-%d" }}</time>
              <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
            </li>
          {% endfor %}
        </ol>
      </section>
      <section class="blog-language-panel" data-language-panel="es" aria-label="Publicaciones en español" hidden>
        <ol class="blog-post-list">
          {% assign spanish_posts = site.posts | where: "lang", "es" %}
          {% for post in spanish_posts %}
            <li>
              <time datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%Y-%m-%d" }}</time>
              <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
            </li>
          {% endfor %}
        </ol>
      </section>
    </div>
  </div>
</div>

<script>
  (() => {
    const root = document.querySelector("[data-blog-language]");
    if (!root) return;

    const buttons = root.querySelectorAll("[data-language-button]");
    const panels = root.querySelectorAll("[data-language-panel]");
    const storageKey = "blog-language";
    let savedLanguage = null;
    try { savedLanguage = localStorage.getItem(storageKey); } catch (_) {}
    const browserLanguage = navigator.language.toLowerCase().startsWith("es") ? "es" : "en";

    function setLanguage(language) {
      buttons.forEach((button) => {
        button.setAttribute("aria-pressed", String(button.dataset.languageButton === language));
      });
      panels.forEach((panel) => {
        panel.hidden = panel.dataset.languagePanel !== language;
      });
      try { localStorage.setItem(storageKey, language); } catch (_) {}
    }

    buttons.forEach((button) => {
      button.addEventListener("click", () => setLanguage(button.dataset.languageButton));
    });
    setLanguage(savedLanguage === "en" || savedLanguage === "es" ? savedLanguage : browserLanguage);
  })();
</script>