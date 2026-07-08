# Agents Guide

Project notes for this Jekyll blog.

## Project Purpose and Tech Stack
- Personal blog for Huy Pham / `coder seventeen`.
- Jekyll static site.
- Markdown content, Sass styling, and small vanilla JS helpers.
- Active runtime pieces: vendored Simple Jekyll Search, Giscus, Font Awesome, Google Fonts, Google Analytics, back-to-top widget.
- No Node package workflow is used.

## Directory Structure Map
- `_posts/` - blog articles.
- `_layouts/` - default, post, page, about, tag, compress layouts.
- `_includes/` - head, inline styles, anchor headings, read-time, share bar, comments.
- `_sass/` - main Sass source.
- `assets/css/` - syntax highlighting CSS.
- `assets/js/` - vendored JS.
- `images/` - logos and blog assets.
- `tag/` - tag landing pages.
- `index.html`, `about.html`, `404.html` - top-level pages.
- `_config.yml` - site config.
- `.github/workflows/jekyll.yml` - build-only CI workflow.

## Active Plugins and Gems
- Gems: `jekyll`, `jekyll-paginate`, `jekyll-sitemap`, `jekyll-relative-links`.
- Plugins enabled in `_config.yml`: `jekyll-paginate`, `jekyll-sitemap`, `jekyll-relative-links`.
- Search script: `assets/js/simple-jekyll-search.js`.

## Local Dev and Build Commands
- Ruby version is pinned to `3.3.4` by `.ruby-version`.
- `bundle install`
- `bundle exec jekyll build`
- `bundle exec jekyll build --future`
- `bundle exec jekyll serve`
- `bundle exec jekyll serve --future`
- Node tooling is intentionally absent; do not run `npm install` or add Node lint/build scripts unless the project becomes Node-managed.

## Deployment Method
- Host target is GitHub Pages.
- GitHub Actions runs a build-only check in `.github/workflows/jekyll.yml`.
- The workflow is intentionally not a custom Pages deploy workflow.
- CI and local verification both use `bundle exec jekyll build --future`.

## Post Front Matter Schema
- `layout: post`
- `title: "..."`
- `description: ...`
- `summary: ...`
- `tags: tag1 tag2`
- Posts live in `_posts/YYYY-MM-DD-slug.md`.
- Keep post images under `images/blog_illustration/` and prefer local asset paths.
- Create tag pages under `tag/<tag-name>/index.html` with `layout: tag` and a matching `tag:` value.

## Sass/CSS Architecture
- Main Sass entry: `_sass/_main.scss`.
- Inline SCSS is injected from `_includes/inline.scss` via `_includes/head.html`.
- Syntax styling comes from `assets/css/syntax.css`.
- Theme colors are controlled through CSS variables and `data-theme`.

## Do-Not-Touch Files
Touch these only with clear intent because they affect global behavior:
- `.ruby-version` - Ruby toolchain version.
- `_config.yml` - site URL, plugins, collections, Giscus, build behavior.
- `_layouts/default.html` - global layout, analytics, theme switcher, search bootstrap.
- `_includes/head.html` - global metadata, CSS loading, feeds.
- `_includes/giscus.html` - comment integration.
- `rss.xml`, `feed.json`, `robots.txt`, `404.html` - site-wide generated/public outputs.

## Known Gotchas
- Keep internal navigation local with `relative_url`; reserve absolute URLs for feeds, sitemaps, canonical metadata, and social sharing.
- GitHub Actions runs `bundle exec jekyll build --future`, while a plain local build may behave differently for future-dated posts.
- Google Analytics is configured by `google_analytics` in `_config.yml`; remove that value to disable it.
- Giscus settings live in `_config.yml` and currently target `coder7eeN/coder7eeN.github.io`.

## Pre-Commit / Lint Checks
- No lint or pre-commit tooling is configured.
- No `eslint`, `stylelint`, `rubocop`, `markdownlint`, or `.pre-commit-config.yaml` was found.
- Before committing, run:
  - `bundle exec jekyll build`
  - `bundle exec jekyll build --future`
  - `bundle exec jekyll serve --future`
  - check homepage, one post, tag page, about page, search, theme toggle, RSS/feed links
- `html-proofer` and `markdownlint` were considered but are not configured. Add them later only if generated HTML/link checks or writing consistency become recurring needs.
