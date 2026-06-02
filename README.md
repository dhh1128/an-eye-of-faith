# An Eye of Faith

[![check site structure](https://github.com/dhh1128/an-eye-of-faith/actions/workflows/check.yml/badge.svg)](https://github.com/dhh1128/an-eye-of-faith/actions/workflows/check.yml)
[![check links](https://github.com/dhh1128/an-eye-of-faith/actions/workflows/link-check.yml/badge.svg)](https://github.com/dhh1128/an-eye-of-faith/actions/workflows/link-check.yml)

*writings on theology by Daniel Hardman*

A small collection of personal theology essays — published with GitHub Pages at
**[dhh1128.github.io/an-eye-of-faith](https://dhh1128.github.io/an-eye-of-faith/)**.

This repository holds the content (Markdown), the owned media (`assets/`), and a
small Python checker that proves the content stays structurally clean. It is a
plain Jekyll site, migrated from a now-defunct WordPress export.

> The cleanup plan and scope live in **[ROADMAP.md](ROADMAP.md)**.

## Quick start

```bash
git clone git@github.com:dhh1128/an-eye-of-faith.git
cd an-eye-of-faith
bundle install
bundle exec jekyll serve     # local preview at http://127.0.0.1:4000/an-eye-of-faith/
```

Run the structural checker — the offline half of the quality gate (Lychee
covers external links in CI):

```bash
pip install pyyaml
python3 scripts/check_site.py
```

## How it's organized

The root-level `*.md` files are the content — one file per essay, filename ==
slug. `index.md` is the site's table of contents (the homepage). Media lives in
`assets/`. **This README is not part of the published site.**

| Path | What |
|---|---|
| `*.md` | essays (one per file) |
| `index.md` | site homepage / table of contents |
| `assets/` | images |
| `scripts/check_site.py` | offline clean-proof (frontmatter, links, assets, WP residue, orphans, search wiring) |
| `_layouts/` `_includes/` `_config.yml` | Jekyll site setup |
| `.github/workflows/` | CI: structural check + external link check |
| `ROADMAP.md` | cleanup plan and scope |

## License

Content is licensed
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.en) unless
otherwise noted.
