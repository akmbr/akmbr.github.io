---
layout: page
permalink: /publications/
title: Papers
description: A list of papers is also available on my [Google Scholar](https://scholar.google.com/citations?user=Rmq3l7gAAAAJ&hl=en).
nav: true
nav_order: 2
---

<!-- _pages/publications.md -->

<!-- Bibsearch Feature -->

{% include bib_search.liquid %}

<div class="publications">

{% bibliography -f submitted --group_by status %}

{% bibliography %}

</div>
