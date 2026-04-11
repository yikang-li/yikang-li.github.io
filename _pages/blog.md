---
layout: default
title: blog
permalink: /blog/
description: Ideas on AI, Data, Science, Finance, and Life.
nav: true
---

<style>
.post-list-container {
  max-width: 800px;
  margin: 0 auto;
}
.post-list-container .post-header {
  margin-bottom: 2.5rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid var(--global-divider-color);
}
.post-list-container .post-title {
  font-size: 2.5rem;
  margin-bottom: 0.5rem;
  color: var(--global-text-color);
}
.post-list-container .post-description {
  color: var(--global-text-color-light);
  font-size: 1rem;
  margin: 0;
}
.post-list-container .post-entry {
  margin-bottom: 2rem;
  padding-bottom: 1.5rem;
  border-bottom: 1px solid var(--global-divider-color);
}
.post-list-container .post-entry:last-child {
  border-bottom: none;
}
.post-list-container .post-date {
  color: var(--global-text-color-light);
  font-size: 0.85rem;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  margin-bottom: 0.4rem;
}
.post-list-container .post-entry-title {
  font-size: 1.5rem;
  font-weight: 600;
  margin: 0 0 0.5rem 0;
  line-height: 1.3;
}
.post-list-container .post-entry-title a {
  color: var(--global-theme-color);
  text-decoration: none;
}
.post-list-container .post-entry-title a:hover {
  text-decoration: underline;
}
.post-list-container .post-entry-desc {
  color: var(--global-text-color);
  opacity: 0.8;
  font-size: 0.95rem;
  line-height: 1.6;
  margin: 0;
}
.post-list-container .post-tags {
  margin-top: 0.5rem;
  font-size: 0.8rem;
  color: var(--global-text-color-light);
}
.post-list-container .post-tag {
  display: inline-block;
  padding: 0.1rem 0.5rem;
  margin-right: 0.3rem;
  background-color: var(--global-code-bg-color);
  border-radius: 3px;
  color: var(--global-text-color-light);
}
</style>

<div class="post-list-container">

  <header class="post-header">
    <h1 class="post-title">{{ site.blog_name }}</h1>
    <p class="post-description">{{ site.blog_description }}</p>
  </header>

  {% for post in site.posts %}
  <div class="post-entry">
    <div class="post-date">{{ post.date | date: "%b %-d, %Y" }}</div>
    <h2 class="post-entry-title"><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
    {% if post.description %}
    <p class="post-entry-desc">{{ post.description }}</p>
    {% endif %}
    {% if post.tags.size > 0 %}
    <div class="post-tags">
      {% for tag in post.tags %}<span class="post-tag">{{ tag }}</span>{% endfor %}
    </div>
    {% endif %}
  </div>
  {% endfor %}

</div>
