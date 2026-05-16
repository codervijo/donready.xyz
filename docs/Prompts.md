# Prompt History — donready.xyz

<!-- Append new prompts at the bottom, newest last. Format:

## YYYY-MM-DD [optional title]
> <prompt text or short summary>

The dated H2 (`## YYYY-MM-DD`) is what `portfolio project status` parses
to surface "last AI prompt" per project. Keep entries append-only.
-->

## 2026-05-08 — scaffolded via portfolio bootstrap

> Created project skeleton. Stack chosen, scaffolding written, git initialized.

## 2026-05-09 — port Lovable export to Astro; fix CF build

> Scoped v1 as a client-side wedge (a few tools + ~10 pages) before pSEO. Hand-ported the Lovable React/TanStack-Start export (`genai/scrub-fit-finder/`) into Astro pages: `/`, `/best-scrubs`, `/compare`, `/figs-vs-mandala`, `/dress-code-checker` (vanilla-JS form), `/scrub-fit-quiz` (vanilla-JS multi-step state machine). Added Tailwind 4, `Base` layout, `SiteHeader`/`SiteFooter`/`CtaBlock`/`Icon` components. Removed `genai/` after Cloudflare Pages failed on its nested-`.git` submodule gitlink.

## 2026-05-16 — fix GSC "sitemap could not be read"

> Astro's sitemap integration emits `/sitemap-index.xml` + `/sitemap-0.xml`, but `robots.txt` and the GSC submission still pointed at the old hand-written `/sitemap.xml` stub — which Cloudflare was serving from edge cache after the file was removed from `dist/`. Pointed `robots.txt` at `/sitemap-index.xml`, deleted the stub from `public/`, and added a `public/_redirects` rule (`/sitemap.xml → /sitemap-index.xml 301`) so the URL Google already has on file keeps resolving instead of 404'ing. Post-deploy steps: purge CF cache for the sitemap/robots URLs, then remove the `sitemap.xml` submission in GSC and add `sitemap-index.xml`.
