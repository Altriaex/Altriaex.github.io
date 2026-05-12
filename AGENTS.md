# AGENTS.md

## Project Overview

This repository is a personal website built with Jekyll on top of the `al-folio` theme.
It is deployed through GitHub Pages and uses `guoxizhang.com` as the custom domain.

Primary stack:

- Jekyll
- Ruby + Bundler
- `al-folio`
- GitHub Actions for deployment

Key repo-level files:

- `_config.yml`: site-wide configuration, metadata, plugins, collections, navigation behavior
- `Gemfile`: Jekyll and plugin dependencies
- `CNAME`: custom domain for GitHub Pages
- `.github/workflows/deploy.yml`: deployment workflow for `main` / `master`
- `README.md`: human-facing project notes

## General Rules

- Ask the user for permission for EVERY code/file change you want to make. DO NOT MODIFY ANY FILE DIRECTLY.
- Treat this repository as a user-maintained website, not as a generic starter template.
- Prefer small, explicit changes over broad theme-level refactors.
- Do not remove user content or generated configuration unless the user explicitly asks for it.
- Before changing layouts, includes, styles, or plugins, explain the likely site-wide impact.
- Do not edit `_site/`; it is generated output.

## Repository Structure

Content directories:

- `_pages/`: top-level site pages such as home and publications
- `_posts/`: blog posts
- `_projects/`: project showcase pages
- `_news/`: news items
- `_bibliography/`: BibTeX source used by `jekyll-scholar`
- `_data/`: structured YAML data such as CV metadata, coauthors, venues, repositories

Rendering and theme directories:

- `_layouts/`: page templates
- `_includes/`: reusable partials and components
- `_plugins/`: local custom Jekyll plugins
- `_sass/`: theme Sass partials
- `assets/css/`: stylesheet entrypoint
- `assets/js/`: frontend scripts
- `assets/img/`: images
- `assets/pdf/`: downloadable PDFs

Operational directories:

- `blog/`: blog listing and pagination entrypoint
- `bin/`: local and deployment helper scripts
- `_site/`: generated static site output; never edit manually
- `.jekyll-cache/`: local build cache
- `.tweet-cache/`: cache for tweet-related content

## Maintenance Guide

Common content updates:

- Update homepage content in `_pages/about.md`
- Update publication page grouping logic in `_pages/publications.md`
- Update publication records in `_bibliography/papers.bib`
- Add or update publication thumbnails by placing compressed images under `assets/img/publication_preview/` and adding `preview = {filename.webp}` to the matching BibTeX entry in `_bibliography/papers.bib`
- Add or edit projects in `_projects/`
- Add or edit blog posts in `_posts/`
- Add or edit news items in `_news/`
- Update profile image and other media under `assets/img/`

Publication thumbnail workflow:

1. Use the paper's project website or a user-provided image as the source.
2. Save any temporary source image inside the repository, preferably as `assets/img/publication_preview/<bibkey>.source.<ext>`, and remove it after generating the final thumbnail.
3. Generate a compressed WebP thumbnail with longest side around 320px and quality around 80. Example:
   `magick <source> -auto-orient -resize '320x320>' -quality 80 assets/img/publication_preview/<bibkey>.webp`
4. Add `preview = {<bibkey>.webp}` to the corresponding entry in `_bibliography/papers.bib`.
5. Remember that homepage selected publications and `/publications/` share `_layouts/bib.html`, so one `preview` field affects both locations.
6. Verify generated dimensions and file size with `magick identify` and `ls -lh`.

Common site-level updates:

- Update name, bio, links, social handles, domain, plugins, and collection settings in `_config.yml`
- Update shared HTML fragments in `_includes/`
- Update page skeletons in `_layouts/`
- Update global styling from `assets/css/main.scss` and related `_sass/` partials

Files that are likely theme defaults or samples:

- Several posts in `_posts/` are sample `al-folio` posts
- Some images and PDFs under `assets/` are theme/demo assets

Before deleting sample content, confirm with the user that it is not intentionally retained.

## Working Conventions For Agents

- Read `_config.yml` before making assumptions about routing, plugins, or collections.
- When changing page content, preserve existing front matter keys unless there is a clear reason to adjust them.
- When adding a new top-level page, check whether `nav: true` and `nav_order` are needed.
- When changing publication behavior, verify both `_pages/publications.md` and `_bibliography/`.
- When changing project cards, verify front matter fields such as `img`, `importance`, and `category`.
- Keep custom domain handling intact unless the user explicitly wants to change the domain.

## Local Development

Typical local workflow:

1. Install Ruby and Bundler if missing.
2. Run `bundle install`.
3. Run `bundle exec jekyll serve`.

Docker-based scripts also exist under `bin/` and can be used if the local Ruby environment is inconvenient.

## Deployment Notes

- The site is configured for GitHub Pages style deployment.
- `CNAME` contains the production domain: `guoxizhang.com`.
- `.github/workflows/deploy.yml` handles deployment from `main` or `master` to `gh-pages`.
- Avoid changing deployment workflow details unless the user asks for deployment-related work.

## al-folio Context

This repository originated from the `al-folio` academic website theme.
Keep that in mind when touching:

- `_layouts/`
- `_includes/`
- `_sass/`
- plugin configuration in `_config.yml`

Theme-level changes can affect multiple page types at once, so agents should explain blast radius before proposing edits.
