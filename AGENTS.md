# AGENTS.md

## What this repo is

- Pure documentation site (Markdown + screenshots) for eScriptorium, published as GitHub Pages (`gh-pages` branch, theme from `_config.yml`).
- No application code, no build, no tests, no lint/typecheck. Verify changes by reviewing rendered Markdown (relative links, image paths, Jekyll theme compatibility).

## Structure

- `index.md` is the Pages landing page and mirrors `README.md` — keep both in sync when adding/renaming guides.
- Guides: `Nutzungsanleitung_eScriptorium.md` (user guide), `Lokale_Installation_eScriptorium.md` (install), `eScriptorium-with-tesseract-extension.md` (EN), `Training-with-eScriptorium-{DE,EN}.md`, `Modellübertragung_Transkribus_nach_eScriptorium.md`.
- `virtual-keyboards/` holds JSON keyboard layouts referenced by the docs.

## Conventions that are easy to get wrong

- German/English guide pairs are **separate files**, and their screenshots are separate images: EN uses `images/training-eS-NN.png`, DE uses `images/training-eS-NN_de.png`. When adding/replacing a screenshot in one language, do the same in the other.
- Screenshots live in `images/` and are referenced with relative `<img src="./images/...">` tags — do not move the directory or use absolute paths.
- Several filenames contain German umlauts (e.g. `Modellübertragung_...`, `Nutzungsanleitung_...`); preserve them exactly.
- `theme: jekyll-theme-cayman` in `_config.yml` drives the published site — keep it.
