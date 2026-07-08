# coder seventeen

Personal Jekyll blog for Huy Pham.

The site started from Gesko, which was forked from [Asko](https://github.com/manuelmazzuola/asko) and inspired by [Klisé](https://github.com/piharpi/jekyll-klise).

## Features

- Responsive Jekyll blog.
- Light and dark themes with saved user preference.
- Inline Sass, syntax highlighting, and anchor headings.
- Tags and tag pages.
- Search with vendored Simple Jekyll Search.
- Atom RSS and JSON feeds.
- Giscus comments and social sharing.

## Local Development

Ruby is pinned to `3.3.4` in `.ruby-version`.

```sh
rbenv install 3.3.4
rbenv local 3.3.4
bundle install
bundle exec jekyll build --future
bundle exec jekyll serve --future
```

Preview at `http://localhost:4000`.

## Deployment

The target host is GitHub Pages at `https://coder7een.github.io`.

The workflow in `.github/workflows/jekyll.yml` is build validation only. It runs `bundle exec jekyll build --future` on pushes and pull requests to `main`; it does not deploy the site.

## Creating a Post

Create a Markdown file under `_posts/` named `YYYY-MM-DD-slug.md`.

```yaml
---
layout: post
title: "Post title"
description: Short SEO/search/share description
summary: Short list/feed summary
tags: fastlane cd
---
```

Post images should live under `images/blog_illustration/`. Prefer local paths such as `/images/blog_illustration/example.png` instead of remote raw GitHub URLs.

## Creating a Tag Page

Create `tag/<tag-name>/index.html` with:

```yaml
---
layout: tag
tag: your-tag
---
```

The tag value should match the post front matter tag exactly.

## Project Notes

This is not a Node-managed project. The search script is vendored in `assets/js/`, and local development uses Ruby, Bundler, and Jekyll only.

Google Analytics is configured in `_config.yml` with `google_analytics`. Remove that value to disable Analytics.

## Contributing

Pull requests for typos, formatting fixes, or site improvements are welcome. Please read [CONTRIBUTING.md](./CONTRIBUTING.md) before opening a PR.

## License

This project is open source and available under the [MIT License](LICENSE.md).
