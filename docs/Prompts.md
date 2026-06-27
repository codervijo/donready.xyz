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

## 2026-05-16 — deploy + GSC submission, plus a UX gotcha worth remembering

> Deployed the fix (commit `360611e`), verified `/sitemap.xml` → `301 → /sitemap-index.xml` after a CF "Purge Everything," and resubmitted `sitemap-index.xml` in GSC. Two observations for future sessions: (1) Cloudflare now injects a "Managed content" block into `robots.txt` at the edge (Content-Signal directives, Disallow for AI crawlers) — origin content is appended *after* it, which is fine but surprising. (2) GSC's Sitemaps page is eventually-consistent in a confusing way: the list-view "Status" column is sticky to the *first* fetch attempt after submission, while the detail panel reflects the most recent read. Submitting before the CF cache has propagated bakes in a "Couldn't fetch" badge that lingers even after GSC successfully re-reads the file. **Lesson: purge CF *before* submitting to GSC, not after.** If this happens again, just remove + re-add the sitemap in GSC to clear the sticky row.

## 2026-06-27 — rewrite figs-vs-mandala for indexing (thin-content → verifiable specifics + JSON-LD)

> Rewrote `/figs-vs-mandala` (`src/pages/figs-vs-mandala.astro`), which Google was crawling but not indexing as thin/generic. Replaced hedged, fabricatable prose with sourced first-hand-quality specifics for FIGS and Mandala — fabric blends, pocket counts, measured inseams, dated June-2026 prices — plus new sections on durability after washes, fluid-resistant/antimicrobial treatments, opacity, tall/petite sizing, shipping/returns, a cross-brand sizing table, honest negatives for both brands, and an authorship/freshness block. Added FAQPage + BreadcrumbList JSON-LD and a visible breadcrumb. Facts were gathered by per-brand web-research agents and verified against official sites; all source URLs logged in `docs/references.md`, and the SEO experiment is tracked in `docs/growth.md` (review 2026-07-25). Two reusable gotchas: (1) WebFetch's text scrape of `wearfigs.com/size-charts` returned hallucinated numbers — the correct chart came from FIGS' size-guide PDF, so verify size data from primary images/PDFs, not scraped text; (2) the shared `sites1` docker container runs in **host network mode**, so `astro dev` on `localhost:4321` is reachable from the host directly — ignore Astro's "use --host to expose" hint, no port publishing needed. Not yet committed or deployed.
