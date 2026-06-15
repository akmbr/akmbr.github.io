---
layout: page
permalink: /notes/
title: Anıl's notes
description: My handwritten notes.
nav: true
nav_order: 4

# ---------------------------------------------------------------------------
# How to add a new note:
#   1. Drop the PDF into  assets/pdf/notes/<your-file>.pdf
#   2. (Optional) Drop a cover image into assets/img/notes/<your-file>.jpg
#        - a single snapshot of the first page works well
#        - leave `thumbnail` blank to fall back to a generic notebook icon
#   3. Add a new entry below. `category` groups notes into sections.
# ---------------------------------------------------------------------------
categories:
  - name: Optimization theory
    description: 
  - name: Statistical learning theory
notes:
  - title: "Gradient Descent, Chebyshev Acceleration, and Krylov Subspace Methods"
    category: Optimization theory
    date: 2026-04-01
    description: 'Various configurations of gradient descent for linear least squares problem and their convergence rates when $\nabla^2 \mathcal{L} \succ 0$. These notes are from the class DSC 243: Advanced Optimization taught by Dmitriy Drusvyatskiy at UCSD.'
    pdf: linear_least_squares.pdf # path relative to assets/pdf/notes/ (or full URL)
    thumbnail: thumbnail_notes_lls.jpeg                    # path relative to assets/img/notes/  (optional)
    pages: 20
    
  - title: "Arnoldi Iteration"
    category: Optimization theory
    date: 2026-04-19
    description: "Arnoldi iteration method to compute maximum eigenvalue of the Hessian. The figure is taken from [this video](https://www.youtube.com/watch?v=2Y1ZDQw_2zw)."
    pdf: Arnoldi_Iteration.pdf
    thumbnail:
    pages: 8
---

<style>
  .notes-grid .card {
    transition: transform .15s ease, box-shadow .15s ease;
  }
  .notes-grid .card:hover {
    transform: translateY(-2px);
  }
  .notes-grid .note-cover {
    aspect-ratio: 3 / 4;
    background: var(--global-card-bg-color, #f6f6f6);
    display: flex;
    align-items: center;
    justify-content: center;
    border-bottom: 1px solid var(--global-divider-color, #eee);
    overflow: hidden;
  }
  .notes-grid .note-cover img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  .notes-grid .note-cover .fallback {
    font-size: 3rem;
    color: var(--global-text-color-light, #999);
  }
  .notes-grid .card-body { padding: 1rem; }
  .notes-grid .card-title a.stretched-link {
    color: inherit;
    text-decoration: none;
  }
  .notes-grid .card-text p { margin-bottom: 0; }
  .notes-grid .card-text a {
    position: relative;
    z-index: 2;
  }
  .notes-grid .note-meta {
    font-size: 0.8rem;
    color: var(--global-text-color-light, #888);
    display: flex;
    justify-content: space-between;
    margin-top: .5rem;
  }
  .notes-category-header {
    margin: 2rem 0 1rem;
    padding-bottom: .3rem;
    border-bottom: 1px solid var(--global-divider-color, #eee);
  }
  .notes-category-header p { margin: 0; font-size: .9rem; color: var(--global-text-color-light, #888); }
</style>

<div class="notes-grid">
{% assign sorted_notes = page.notes | sort: "date" | reverse %}

{% for cat in page.categories %}
  {% assign cat_notes = sorted_notes | where: "category", cat.name %}
  {% if cat_notes.size > 0 %}
    <div class="notes-category-header">
      <h2 class="category text-lowercase">{{ cat.name }}</h2>
      {% if cat.description %}<p>{{ cat.description }}</p>{% endif %}
    </div>

    <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 g-3">
      {% for note in cat_notes %}
        {% if note.pdf contains '://' %}
          {% assign pdf_url = note.pdf %}
        {% else %}
          {% assign pdf_url = note.pdf | prepend: '/assets/pdf/notes/' | relative_url %}
        {% endif %}
        <div class="col mb-3">
          <div class="card h-100 hoverable position-relative">
            <div class="note-cover">
              {% if note.thumbnail %}
                <img src="{{ note.thumbnail | prepend: '/assets/img/notes/' | relative_url }}" alt="{{ note.title }} cover">
              {% else %}
                <span class="fallback"><i class="fa-regular fa-file-lines"></i></span>
              {% endif %}
            </div>
            <div class="card-body">
              <h3 class="card-title" style="font-size:1rem; margin-bottom:.35rem;">
                <a href="{{ pdf_url }}" class="stretched-link" target="_blank" rel="noopener">{{ note.title }}</a>
              </h3>
              {% if note.description %}
                <div class="card-text" style="font-size:.85rem; margin-bottom:0;">{{ note.description | markdownify }}</div>
              {% endif %}
              <div class="note-meta">
                <span><i class="fa-regular fa-calendar"></i> {{ note.date | date: "%b %Y" }}</span>
                {% if note.pages %}<span>{{ note.pages }} pp.</span>{% endif %}
              </div>
            </div>
          </div>
        </div>
      {% endfor %}
    </div>
  {% endif %}
{% endfor %}

{% assign uncategorized = sorted_notes | where_exp: "n", "n.category == nil" %}
{% if uncategorized.size > 0 %}
  <div class="notes-category-header"><h2 class="category text-lowercase">other</h2></div>
  <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 g-3">
    {% for note in uncategorized %}
      {% if note.pdf contains '://' %}{% assign pdf_url = note.pdf %}{% else %}{% assign pdf_url = note.pdf | prepend: '/assets/pdf/notes/' | relative_url %}{% endif %}
      <div class="col mb-3">
        <div class="card h-100 hoverable position-relative">
          <div class="note-cover">
            {% if note.thumbnail %}
              <img src="{{ note.thumbnail | prepend: '/assets/img/notes/' | relative_url }}" alt="{{ note.title }} cover">
            {% else %}
              <span class="fallback"><i class="fa-regular fa-file-lines"></i></span>
            {% endif %}
          </div>
          <div class="card-body">
            <h3 class="card-title" style="font-size:1rem; margin-bottom:.35rem;">
              <a href="{{ pdf_url }}" class="stretched-link" target="_blank" rel="noopener">{{ note.title }}</a>
            </h3>
            {% if note.description %}<div class="card-text" style="font-size:.85rem; margin-bottom:0;">{{ note.description | markdownify }}</div>{% endif %}
            <div class="note-meta">
              <span><i class="fa-regular fa-calendar"></i> {{ note.date | date: "%b %Y" }}</span>
              {% if note.pages %}<span>{{ note.pages }} pp.</span>{% endif %}
            </div>
          </div>
        </div>
      </div>
    {% endfor %}
  </div>
{% endif %}
</div>
