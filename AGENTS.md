# AGENTS.md

## What this repo is

- Pure documentation site (Markdown + screenshots) for eScriptorium, published as GitHub Pages (`gh-pages` branch, theme from `_config.yml`).
- No application code, no build, no tests, no lint/typecheck. Verify changes by reviewing rendered Markdown (relative links, image paths, Jekyll theme compatibility).

## Structure

- `index.md` is the Pages landing page and mirrors `README.md` — keep both in sync when adding/renaming guides (both group guides into "Neue Oberfläche" and "Legacy-Oberfläche").
- Guides: `Nutzungsanleitung_eScriptorium.md` (legacy user guide), `Nutzungsanleitung_neues_Interface_eScriptorium.md` (new-interface guide), `Lokale_Installation_eScriptorium.md` (install, current), `eScriptorium-with-tesseract-extension.md` (EN, legacy), `Training-with-eScriptorium-{DE,EN}.md` (legacy), `Modellübertragung_Transkribus_nach_eScriptorium.md` (legacy).
- `virtual-keyboards/` holds JSON keyboard layouts referenced by the docs.

## Conventions that are easy to get wrong

- Docs are split by **interface generation**: legacy UI (eScriptorium pre-1.0) vs new UI (introduced in 1.0). Note the latest eScriptorium release supports **both** UIs — the guides describe two UIs, not two versions. Keep each guide's scope note (top blockquote) and its section in `README.md`/`index.md` consistent with that split.
- Local screenshots are referenced with relative `<img src="./images/...">` tags (no absolute paths, no moving the dir). They live in `images/legacy/` (legacy-UI screenshots) and `images/current/` (current-UI screenshots). Some older guides (e.g. the main `Nutzungsanleitung_eScriptorium.md`) reference external `user-images.githubusercontent.com` URLs instead of local files — leave those alone.
- The German/English training guides are separate files with separate legacy screenshots: EN uses `images/legacy/training-eS-NN.png`, DE uses `images/legacy/training-eS-NN_de.png`. When adding/replacing a screenshot in one language, do the same in the other.
- Several filenames contain German umlauts (e.g. `Modellübertragung_...`, `Nutzungsanleitung_...`); preserve them exactly.
- `theme: jekyll-theme-cayman` in `_config.yml` drives the published site — keep it.
