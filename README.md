# mjrodriguez.github.io

Personal website and blog built with [Jekyll](https://jekyllrb.com/) and hosted on GitHub Pages.

## Prerequisites

- Ruby (any recent version; the system Ruby on macOS works fine)
- Bundler: `gem install bundler`

## Install

```bash
bundle install
```

## Run locally

```bash
bundle exec jekyll serve
```

Open [http://localhost:4000](http://localhost:4000) in your browser.

> If you edit `_config.yml`, restart the server — Jekyll does not hot-reload it.

## Build

```bash
bundle exec jekyll build
```

Output is written to `_site/`.

## Adding a blog post

Create a file in `_posts/` named `YYYY-MM-DD-your-title.markdown`:

```yaml
---
layout: post
title: "Your Post Title"
date: YYYY-MM-DD HH:MM:SS -0700
categories: tag1 tag2
---

Post content goes here. Inline math: $E = mc^2$. Block math:

$$
\int_a^b f(x)\,dx
$$
```

## Project structure

| Path | Purpose |
|---|---|
| `_config.yml` | Site settings (title, author, nav, plugins) |
| `_posts/` | Blog posts in Markdown |
| `_layouts/default.html` | Base HTML layout; loads MathJax |
| `_includes/` | Partial templates (head, footer, social) |
| `_sass/minima.scss` | Custom CSS overrides |
| `assets/` | Images and favicon |
| `*.markdown` | Top-level pages (index, about, research, teaching, blog) |
