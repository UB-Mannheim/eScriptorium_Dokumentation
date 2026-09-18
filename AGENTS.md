# AGENTS.md

## What this repo is

- Pure documentation site (Markdown + screenshots) for eScriptorium, published as GitHub Pages with the **Just the Docs** theme (`theme: just-the-docs` in `_config.yml`).
- The site is built by the GitHub Pages Actions workflow (`.github/workflows/jekyll-docker.yml`), which needs the `Gemfile` (pins `just-the-docs`). Verify changes by building the site locally, e.g. with the official Jekyll container image via podman: `podman run --rm -v "$PWD":/src -w /src jekyll/jekyll:pages sh -c "bundle install && bundle exec jekyll build"` (check that all guides appear in `_site/` with working image paths, internal links, and `_site/search-data.json`).

## Structure

- `index.md` is the Pages landing page and mirrors `README.md` — keep both in sync when adding/renaming guides (both group guides into "Neue Oberfläche" and "Legacy-Oberfläche").
- Section pages `neue-oberflaeche.md` / `legacy-oberflaeche.md` hold the grouped guide lists (and serve as the sidebar parents, see below).
- Guides: `Nutzungsanleitung_eScriptorium.md` (legacy user guide), `Nutzungsanleitung_neues_Interface_eScriptorium.md` (new-interface guide; section 4 "Zusätzliche Funktionen der Mannheim-Instanz" documents the Mannheim new-UI additions: baseline editing + cut mode §4.1, transcription font §4.2, language selector §4.3), `Lokale_Installation_eScriptorium.md` (install, current), `eScriptorium-with-tesseract-extension.md` (EN, legacy), `Training-with-eScriptorium-{DE,EN}.md` (legacy), `Modellübertragung_Transkribus_nach_eScriptorium.md` (legacy), `administration.md` (admin: transcription fonts, Matomo analytics — top-level sidebar entry, `nav_order: 3`, no `parent`).
- `virtual-keyboards/` holds JSON keyboard layouts referenced by the docs.

## Conventions that are easy to get wrong

- Docs are split by **interface generation**: legacy UI (eScriptorium pre-1.0) vs new UI (introduced in 1.0). Note the latest eScriptorium release supports **both** UIs — the guides describe two UIs, not two versions. Keep each guide's scope note (top blockquote) and its section in `README.md`/`index.md` consistent with that split.
- Local screenshots are referenced with relative `<img src="./images/...">` tags (no absolute paths, no moving the dir). They live in `images/legacy/` (legacy-UI screenshots) and `images/current/` (current-UI screenshots). Some older guides (e.g. the main `Nutzungsanleitung_eScriptorium.md`) reference external `user-images.githubusercontent.com` URLs instead of local files — leave those alone.
- The German/English training guides are separate files with separate legacy screenshots: EN uses `images/legacy/training-eS-NN.png`, DE uses `images/legacy/training-eS-NN_de.png`. When adding/replacing a screenshot in one language, do the same in the other.
- Several filenames contain German umlauts (e.g. `Modellübertragung_...`, `Nutzungsanleitung_...`); preserve them exactly.
- `theme: just-the-docs` in `_config.yml` drives the published site — keep it. `README.md` is excluded from the build; keep `index.md` as the landing page.
- **The sidebar is built from page front matter, not from `_config.yml`** (JTD 0.12.0 has no `nav:` option — such a block is silently ignored). Each guide needs a unique `title:` plus `parent:` + `nav_order:`. The two section pages `neue-oberflaeche.md` ("Neue Oberfläche (ab eScriptorium 1.0)") and `legacy-oberflaeche.md` ("Legacy-Oberfläche (Versionen vor eScriptorium 1.0)") act as the nav parents and hold the guide lists. `index.md` has `nav_exclude: true`. When adding/renaming guides, update their front matter, the matching section page, `README.md`, and `index.md`.
- The UI is German-first: page titles/nav labels/search placeholder are in German; the site footer is set in `_includes/nav_footer_custom.html` (non-empty, or JTD prints an English "This site uses Just the Docs" line) — it credits "Universitätsbibliothek Mannheim und die Autor:innen" (contributors include non-Mannheim authors) plus the repo's CC0 1.0 license (see `LICENSE`). English guides are labeled "(englisch)" in nav and lists.
- The browser favicon is `favicon.ico` in the repo root (the eScriptorium logo, a 32×32 PNG in `.ico` clothing) — JTD picks up `/favicon.ico` automatically.
- Theme look-and-feel tweaks live in `_sass/custom/custom.scss` (appended after all theme styles, so `!important` overrides win): the sidebar keeps its base width on wide screens, the root font size is raised (16px -> 18px, which scales the rem-based content typography), and nav font sizes are bumped (links 16px, categories 14px).
