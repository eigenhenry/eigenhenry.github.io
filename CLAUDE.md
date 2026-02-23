# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is Henry Salgado's personal academic website built with the [Academic Pages](https://github.com/academicpages/academicpages.github.io) Jekyll template, hosted on GitHub Pages. The actual site lives in the `eigenhenry.github.io/` subdirectory.

## Development Commands

All commands should be run from within `eigenhenry.github.io/`.

**Install dependencies:**
```bash
bundle install
```

**Serve locally with live reload:**
```bash
jekyll serve -l -H localhost
```
Site is available at `http://localhost:4000`. Note: `_config.yml` changes require restarting the server.

**Using Docker instead:**
```bash
docker build -t jekyll-site .
docker run -p 4000:4000 --rm -v $(pwd):/usr/src/app jekyll-site
```

**Generate markdown from TSV data (publications/talks):**
```bash
# From markdown_generator/
python publications.py   # or run publications.ipynb
python talks.py          # or run talks.ipynb
```

## Architecture

The repo root holds a top-level `Gemfile` (just `gem "jekyll"`). The real site is `eigenhenry.github.io/` with its own `Gemfile` and `Dockerfile`.

### Content Collections (YAML front matter → rendered pages)

Content is stored as markdown files with YAML front matter. Each collection drives multiple views automatically (listing pages, individual pages, CV section):

| Directory | URL pattern | Key front matter fields |
|---|---|---|
| `_publications/` | `/publication/<slug>` | `title`, `venue`, `date`, `category` (`manuscripts`/`conferences`/`books`), `paperurl`, `slidesurl`, `arxivurl`, `doi`, `citation` |
| `_talks/` | `/talks/<slug>` | `title`, `type`, `venue`, `date`, `location` |
| `_posts/` | `/:categories/:title/` | standard Jekyll post front matter |
| `_teaching/` | `/teaching/<slug>` | `title`, `type`, `venue` |
| `_portfolio/` | `/portfolio/<slug>` | `title`, `excerpt` |

### Key Configuration Files

- `_config.yml` — Site-wide settings: author info, social links, plugins, collection permalinks, Sass config
- `_data/navigation.yml` — Top nav links (order and visibility)
- `_data/ui-text.yml` — Localization strings
- `_pages/` — Static pages (about/home, CV, publications list, talks list, etc.)

### Theme Structure

- `_layouts/` — Page templates (`single.html`, `archive.html`, `talk.html`, `default.html`)
- `_includes/` — Reusable partials (author sidebar, masthead, SEO tags, social share, comments)
- `_sass/` — Sass stylesheets (compiled from `_sass/` into compressed CSS)
- `assets/` — Static assets (JS, CSS output, images)

### Markdown Generator Workflow

To batch-add publications or talks, edit the TSV files in `markdown_generator/` (`publications.tsv`, `talks.tsv`) and run the corresponding Python scripts or Jupyter notebooks to generate the individual markdown files in `_publications/` or `_talks/`.

### Static Files

- `files/` — PDFs and downloadable files, accessible at `/files/<filename>`
- `images/` — Site images referenced in markdown

### Publication Link Fields

Publications support these optional link fields in front matter:

| Field | Effect |
|---|---|
| `arxivurl` | Full arXiv URL (e.g. `https://arxiv.org/abs/2601.21221`) |
| `doi` | DOI identifier only (e.g. `10.48550/arXiv.2601.21221`), auto-prefixed with `https://doi.org/` |
| `paperurl` | Direct PDF or paper URL |
| `slidesurl` | Slides URL |

`arxivurl` → `doi` → `paperurl` is the priority order for the external link icon shown next to the title in the publications listing (`_includes/archive-single.html`). All present fields render as links on the individual paper page (`_layouts/single.html`).
