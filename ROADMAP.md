# Roadmap

Cleanup plan for the An Eye of Faith theology-essay site after its migration
from a (now-defunct) WordPress export to Jekyll + GitHub Pages.

_Created 2026-06-02._

## Scope decision

This is a small personal creative/theology site — twelve essays — not a book or
a professional anthology. A sister repo, `../sivanea.com`, went through this same
cleanup, and a further-removed cousin (`../codecraft.co`) went through a much
larger arc (a multi-essay software anthology groomed into an Amazon KDP **book**:
permanent item-IDs, a controlled tag vocabulary, a full metadata schema, per-essay
PDFs, a platform migration). **None of that heavy machinery ports here.**

So the goal is narrow: **fix the genuine breakage, and stand up a lightweight,
proportionate proof that the content is and stays clean.** Every quality goal is a
script plus a check that CI runs; green == publishable.

This repo is a GitHub Pages **project site** (no custom domain), served under the
`/an-eye-of-faith/` path prefix — the main divergence from sivanea (a root domain).
Anything that must resolve a path is therefore baseurl-aware.

## Done

- [x] **Gemfile.** The repo had none, so `bundle exec jekyll build` could not run.
      Added Jekyll 4.2 + remote-theme, sitemap, seo-tag, webrick, and
      `jekyll-redirect-from` (every page carries `redirect_from` frontmatter).
- [x] **Stripped WordPress-era markup.** Removed a leftover `wp-image…` class and a
      `?w=1024` resize query, and moved inline `style=` attributes to semantic CSS
      classes (`.text-right`, `.indented`). Mechanical only — no prose changed.
- [x] **README / homepage split.** `README.md` had doubled as both the GitHub
      landing page and the published flat TOC. Split into `index.md`
      (`permalink: /`, the reader-facing Contents + search) and a GitHub-facing
      `README.md` (badges, quickstart, repo-layout table, license). `README.md` and
      `ROADMAP.md` are excluded from the build.
- [x] **Homepage full-text search.** A live search box on `index.md` powered by
      vendored Lunr.js (`assets/js/lunr.min.js`) + a Liquid-generated `search.json`
      index + `assets/js/search.js`. Stemmed **and** trailing-wildcard query per
      term; the index URL is passed in via a `data-index` attribute so it resolves
      under the baseurl. Degrades to the plain Contents list with no JS.
- [x] **Proof harness.** `scripts/check_site.py` — offline, Jekyll-aware checker
      proving frontmatter validity + non-empty titles, internal page/asset link
      resolution, no WordPress residue (incl. `zem_slink`/`wp-image`), no stray CI
      badge on a published page, no orphan pages, and the search wiring. Wired into
      CI via `.github/workflows/check.yml` (`checkout@v6` + `setup-python@v6`).
- [x] **Made link-check meaningful.** Moved `link-check.yml` from the repo root
      (where GitHub never ran it) into `.github/workflows/`, bumped
      `lycheeverse/lychee-action` to `v2.8.0` and `actions/checkout` to `v6`, and
      added `.github/lychee.toml` (extensionless-link remap, excludes for hosts that
      bot-block automated checkers, tolerate `429`).
- [x] **A "← back" link** at the top of every page (baseurl-aware, hidden in print).
- [x] **Print stylesheet.** Hide nav chrome and render images centered at ~half the
      text-column width to save ink.
- [x] **Layout faithfulness.** Added a `defaults` layout block so local builds match
      GitHub Pages, set `baseurl`, and fixed the favicon reference.
- [x] **Deleted the inert `tools/`** WordPress-migration scripts (git history is the
      archive).

## Standing policy (decided)

- **External images stay.** A handful of credited artwork/photo references point
  off-site; the goal is "external images still resolve" (Lychee verifies this in
  CI), not "own 100% of images." The checker reports the count for awareness but
  never fails on it.
- **Mechanical edits only.** Fix structure, links, images, metadata, config; never
  rewrite the author's prose.

## Deliberately NOT doing (ported from the cousin repos, but not warranted here)

- Permanent item-IDs, a controlled tag vocabulary, a rich metadata schema, per-item
  PDFs, the book/KDP pipeline, and any platform migration. No goal here drives them.
- Rendering reader comments. The layout has no comments section; the migrated
  `comments:` frontmatter stays dormant data rather than being surfaced.
