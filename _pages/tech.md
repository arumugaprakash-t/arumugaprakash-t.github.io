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
    margin-bottom: 2rem;
    padding-bottom: 1.5rem;
    border-bottom: 1px solid #e5e5e5;
  }
  .post-item:last-child {
    border-bottom: none;
  }
  .post-link {
    font-size: 1.5rem;
    font-weight: 600;
    color: #2c3e50;
    text-decoration: none;
    transition: color 0.2s;
  }
  .post-link:hover {
    color: #dc3545;
  }
  .post-meta {
    font-size: 0.9rem;
    color: #6c757d;
    margin-bottom: 0.5rem;
  }
  .post-excerpt {
    color: #444;
    line-height: 1.6;
    margin-top: 0.5rem;
  }
  .read-more {
    color: #dc3545;
    text-decoration: none;
    font-weight: 500;
    font-size: 0.95rem;
  }
  .read-more:hover {
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
