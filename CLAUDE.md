# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Personal academic website for Zerui Liu (Ph.D. candidate, NAOC/CAS), built on the
[academicpages](https://github.com/academicpages/academicpages.github.io) Jekyll theme. Content lives in
Markdown/YAML front matter, not in templates — editing content means editing `_pages/`, `_publications/`,
`_talks/`, `_data/`, and `_config.yml`. The theme machinery under `_includes/`, `_layouts/`, `_sass/`,
`assets/` is upstream template code and is rarely the right place to make a change (prefer front matter or
inline page HTML/CSS).

Deployed to GitHub Pages at <https://lrayleighj.github.io> by `.github/workflows/jekyll.yml` on every push
to `master` (Ruby 3.1, `bundle exec jekyll build` → `upload-pages-artifact`/`deploy-pages`).

`README.md` (Chinese) documents the content-editing workflows in more detail and is the source of truth for
intent; `AGENTS.md` is the upstream template's own note to agents.

## Building and previewing

**Ruby, Bundler and Jekyll are not installed on this machine** (verified: `ruby`, `bundle`, `jekyll` are all
absent from `PATH`; `node`, `npm` and `python3` are present). There is therefore no way to build or preview
the site locally without installing a toolchain first, and no test suite or configured lint script exists.
Consequence: **changes cannot be build-verified locally by default.** Either read carefully and let CI build
on push, or pick one of these to get a real build:

```sh
# Option A — native Ruby 3.x
bundle install
bundle exec jekyll serve          # http://localhost:4000 ; add -l for live reload
bundle exec jekyll build          # output to _site/

# Option B — Docker / devcontainer (ruby:3.2 image, no host Ruby needed)
docker compose up -d && docker compose exec jekyll-site jekyll serve -H 0.0.0.0 -w --config _config.yml,_config_docker.yml
```

`_config_docker.yml` only blanks `url:` so localhost links work; the devcontainer's `postCreateCommand` runs
the same serve command. `_config.yml` is **not** reloaded by `jekyll serve` — restart the server after
changing it.

```sh
# JS bundle — only needed after editing assets/js/_main.js or assets/js/theme.js
npm install && npm run build:js   # uglify -> assets/js/main.min.js (checked in)

# Markdown generators (stdlib-only Python; see markdown_generator/README.md)
cd markdown_generator && python3 publications.py publications.csv   # writes ../_publications/
python3 markdown_generator/talks.py markdown_generator/talks.tsv   # writes _talks/
```

Note the asymmetry: `publications.py` writes to `../_publications/` relative to the **current working
directory**, so it must be run from inside `markdown_generator/`; `talks.py` resolves its paths from
`__file__` and also takes an optional output directory. Current `_publications/` and `_talks/` entries were
hand-written and do not round-trip through these generators.

## Content architecture

### Front matter drives everything

Pages are rendered by Liquid loops over collections, not by listing content:

- [`_pages/publications.html`](_pages/publications.html) iterates `site.publication_category` (defined in
  `_config.yml`) and emits an `<h2>` heading per category, filtering entries on their `category:` front matter.
- [`_pages/cv.md`](_pages/cv.md) filters the same collection into two lists (`manuscripts` vs `preprints`)
  using `archive-single-cv.html`, so a publication appears on both the publications page and the CV.
- [`_pages/talks.html`](_pages/talks.html) loops `site.talks reversed`.

Because of this, a **`category:` value in `_publications/*.md` must match a key under `publication_category`
in `_config.yml`** — a typo means the entry silently renders nowhere. Likewise a new collection needs both a
`collections:` entry and a `defaults:` scope in `_config.yml`.

### Ordering is by `date:`, reversed

`date:` in publications and talks is an approximate sort key derived from publication year/volume, not a
precise date. Reorder an entry by changing its `date:`, not by moving files. Filenames are
`YYYY-MM-DD-slug.md` and each publication carries an explicit
`permalink: /publication/<same date>-<same slug>` (singular `/publication/`, while the archive page is at
plural `/publications/`). Keep filename and permalink in sync when renaming; changing the permalink breaks
existing links.

### `archive-single.html` special-cases preprints

[`_includes/archive-single.html`](_includes/archive-single.html) renders `"Published in <venue>"`
for `manuscripts` but plain `"<venue>, <year>"` for `category: preprints`. It also chooses the trailing link
line from which of `citation` / `paperurl` / `slidesurl` / `bibtexurl` are present. `paperurl` currently holds
DOI URLs (publisher landing pages, not direct PDFs).

### Author sidebar, navigation, avatar, downloads

- `_config.yml` → `author:` block feeds the sidebar via `_includes/author-profile.html`; `avatar:
  "profile.jpg"` resolves to `/images/profile.jpg`. `_data/authors.yml` is only consulted for an explicit
  `author: <key>` in a page's front matter.
- [`_data/navigation.yml`](_data/navigation.yml) controls the masthead order; removing a link hides it
  without affecting the page. The home page is `_pages/about.md` with `permalink: /`, and both it and
  `_pages/cv.md` use `redirect_from:` (requires the already-enabled `jekyll-redirect-from` plugin).
- `files/` is in `_config.yml`'s `include:`, so anything dropped there is served at `/files/<name>`.
- Template leftovers not in the nav and safe to ignore: `_pages/sitemap.md`, `_pages/terms.md`,
  `_pages/404.md`, and the whole `talkmap/` directory (excluded from the build; `talkmap_link: false`).

### Theme selection

`site_theme` in `_config.yml` is interpolated by Liquid inside
[`assets/css/main.scss`](assets/css/main.scss) as `theme/{{ site.site_theme }}_light` and `_dark`. Changing
the theme name therefore requires the matching **pair** in `_sass/theme/` (`_<name>_light.scss` +
`_<name>_dark.scss`); available pairs are air, contrast, default, dirt, mint, sunrise. Dark mode is applied
by `data-theme="dark"` on `<html>` in `_layouts/default.html`.

### Photography page

`_pages/photography.md` is a standalone page with its own inline `<style>` and hand-written
`<a class="photo">…</a>` blocks grouped under `<h2>` headings. Full-size images live in `photos/` (served
directly, filename is the URL); grid thumbnails live in `photos/thumbs/` at 800px long edge / quality 68,
generated with macOS `sips` (not available on this Linux machine — use ImageMagick/`convert` here, or
regenerate elsewhere). Thumbnails use `object-fit: cover` so grid cells are uniform, but originals are never
cropped. Adding a photo means adding both files plus one `<a class="photo">` block with a descriptive `alt`.

### The `exclude:` list is load-bearing

`_config.yml`'s `exclude:` already lists `Dockerfile`, `Gemfile`, `README`, `AGENTS.md`, `markdown_generator`,
`talkmap*`, `node_modules`, etc. **Any new top-level development file or directory must be added there**, or
Jekyll will publish it to the live site.

## Content constraints

Two first-author papers (FAST × DESI cross-correlation; HI density parameter in IllustrisTNG) are in
preparation and their entries in `_publications/` are **deliberately sanitized**: title, one-sentence
description, and no numerical results, no `files/` drafts. Keep it that way until they are published or on
arXiv. For the same reason, do not link `cv_zerui.pdf`/`cv.tex` into `files/` — the full CV contains the
unpublished numbers, and publishing it would re-expose them. When in doubt, confirm before adding anything
that states unpublished results.
