# Prioritized Implementation Checklist

## P0 - Ruby 3.3.4 and Build Reliability
- [x] Install Ruby `3.3.4` locally with `rbenv`, `rvm`, or another Ruby version manager.
- [x] Update `.ruby-version` from `2.7.2` to `3.3.4`.
- [x] Run `ruby -v` from repo root and confirm it uses `3.3.4`.
- [x] Run `bundle install`.
- [x] If dependency resolution fails, run `bundle update`.
- [x] Verify `Gemfile.lock` updates cleanly.
- [x] Run `bundle exec jekyll build`.
- [x] Run `bundle exec jekyll build --future`.
- [x] Run `bundle exec jekyll serve --future`.
- [x] Manually check homepage, about page, one post page, one tag page, search, theme toggle, and RSS/feed links.
- [x] Update `docs/agents.md` to explicitly say Ruby `3.3.4`.
- [x] Update `README.md` local setup if needed.

## P1 - Fix Current Runtime and HTML Issues
- [x] Fix invalid HTML in `index.html`, especially stray `</p>` tags.
- [x] Fix theme fallback logic in `_layouts/default.html` so system preference works.
- [x] Make sure theme toggle still persists user choice in `localStorage`.
- [x] Re-run `bundle exec jekyll build --future`.
- [x] Re-check homepage rendering after HTML cleanup.
- [x] Re-check one post page and one tag page for layout regressions.

## P1 - Make URLs Local and Deployment Safe
- [x] Audit internal links using `site.url`.
- [x] Replace internal navigation links with `relative_url`.
- [x] Keep absolute URLs only where needed for feeds, sitemap, canonical URLs, or social sharing.
- [x] Review `index.html`, `_layouts/post.html`, `_layouts/tag.html`, `_layouts/about.html`, `_layouts/default.html`, `_includes/head.html`, and `_includes/share_bar.html`.
- [x] Verify local preview works at `localhost:4000`.
- [x] Verify generated links still work for GitHub Pages root deployment.

## P2 - Deployment and Config Cleanup
- [x] Decide final deployment model: GitHub Pages default build or custom GitHub Actions deploy.
- [x] If keeping current model, document that Actions is build-only.
- [x] If using custom Actions deploy, replace the current workflow with an explicit Pages deploy workflow.
- [x] Align CI command with local verification: `bundle exec jekyll build --future`.
- [x] Move hardcoded Google Analytics ID from `_layouts/default.html` into `_config.yml`, or remove it if unused.
- [x] Confirm Giscus config in `_config.yml` is still valid.
- [x] Review `_config.yml` values: `url`, `baseurl`, `future`, `published`, `timezone`, `lang`.

## P2 - Project Metadata Cleanup
- [x] Decide whether Node tooling is needed.
- [x] If Node is not needed, remove the misleading `package.json` and `package-lock.json`.
- [x] If Node is needed, create a valid `package.json` with scripts and dependencies.
- [x] Document the final decision in `docs/agents.md`.
- [x] Re-run Jekyll build after metadata cleanup.

## P3 - SEO and Metadata
- [x] Add or improve page metadata in `_includes/head.html`.
- [x] Add canonical URL handling.
- [x] Add Open Graph metadata.
- [x] Add Twitter card metadata.
- [x] Ensure posts consistently use `description`.
- [x] Check generated homepage and post HTML metadata.
- [x] Re-run `bundle exec jekyll build --future`.

## P3 - Lightweight Quality Checks
- [x] Keep manual pre-commit checks in `docs/agents.md`.
- [x] Add CI build validation if not already reliable after Ruby upgrade.
- [x] Consider adding `html-proofer` for generated HTML and link checks.
- [x] Consider adding `markdownlint` only if writing consistency becomes important.
- [x] Avoid Node-based lint tooling unless the project becomes a real Node-managed repo.

## P4 - Content and Maintenance Polish
- [x] Update `README.md` so setup instructions match this repo, not the original template.
- [x] Fix README typos and outdated deployment guidance.
- [x] Document how to create a new post.
- [x] Document how to create a new tag page.
- [x] Normalize image conventions under `images/blog_illustration/`.
- [x] Replace remote raw GitHub image URLs with local asset paths where practical.
- [x] Review old posts for broken images or obsolete links.

## Assumptions
- Ruby target is `3.3.4`.
- Hosting remains GitHub Pages unless explicitly changed.
- The current custom Jekyll theme stays in place.
- No new Node tooling should be added unless there is a clear need.
