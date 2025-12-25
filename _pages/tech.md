---
layout: page
title: Tech
permalink: /tech/
description: Technical writings and projects
---

<style>
  .post-list {
    list-style: none;
    padding: 0;
    margin: 2rem 0;
  }
  .post-item {
    margin-bottom: 2.5rem;
    padding-bottom: 2rem;
    border-bottom: 1px solid var(--color-border);
  }
  .post-item:last-child {
    border-bottom: none;
  }
  .post-link {
    font-size: 1.25rem;
    font-weight: 500;
    color: var(--color-black);
    text-decoration: none;
    transition: color 0.2s;
    letter-spacing: -0.01em;
  }
  .post-link:hover {
    color: var(--color-gray);
  }
  .post-meta {
    font-size: 0.875rem;
    color: var(--color-light-gray);
    margin-bottom: 0.75rem;
  }
  .post-excerpt {
    color: var(--color-charcoal);
    line-height: 1.6;
    margin-top: 0.75rem;
    font-size: 1.0625rem;
  }
  .read-more {
    color: var(--color-black);
    text-decoration: none;
    font-weight: 500;
    font-size: 0.9375rem;
    transition: color 0.2s;
  }
  .read-more:hover {
    color: var(--color-gray);
    text-decoration: underline;
  }
</style>

<div class="blog-posts">
  <ul class="post-list">
    {% for post in site.posts %}
      {% if post.categories contains 'tech' or post.categories contains 'databases' %}
        <li class="post-item">
          <div class="post-meta">{{ post.date | date: "%B %d, %Y" }}</div>
          <h2><a href="{{ post.url | relative_url }}" class="post-link">{{ post.title }}</a></h2>
          {% if post.description %}
            <p class="post-excerpt">{{ post.description }}</p>
          {% else %}
            <p class="post-excerpt">{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
          {% endif %}
          <a href="{{ post.url | relative_url }}" class="read-more">Read more →</a>
        </li>
      {% endif %}
    {% endfor %}
  </ul>
</div>
