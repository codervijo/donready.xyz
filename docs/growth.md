# Growth Log — donready.xyz

> **What this file is for:** an honest, append-only log of growth experiments
> on this site — what was tried, what was measured, what happened. The data
> source is GSC; this file narrates *why*. Future-you (or future-Claude)
> reads this when deciding what to try next, both on this site and on
> related sister sites.

## How to use this (workflow — re-read this when you forget)

**Add an entry whenever you do something growth-relevant.** That includes:
shipping new content, structural SEO changes (sitemap, schema, redirects,
internal linking), tech changes that affect crawl/indexing, marketing
pushes, backlink campaigns. *Not* every code commit — just things you'd
want to point at when GSC numbers move (or fail to).

**Each entry is a hypothesis you can be wrong about.** Commit to a
measurable KPI and an observation window before acting — otherwise "did
this work?" is just a feeling.

### Lifecycle of one entry

1. **Day of action** — append a new dated H2 with `Status: active`, the
   hypothesis, the KPI you'll watch, current baseline numbers, what you
   did, and the date to review (default: today + 28 days, matching GSC's
   reporting window).
2. **Review day** — pull current GSC numbers, compute delta vs baseline.
   Fill in **Result** and **Learning**. Set **Status** to `shipped` (worked,
   keep going), `failed` (didn't pay off, abandon), or extend the review
   another window if results are ambiguous.
3. **Never rewrite older entries.** Wrong hypotheses are the most valuable
   data — they tell you what NOT to repeat on the next site. Append, don't
   edit.

### Where to get the numbers

```bash
cd ~/work/projects/sites/portfolio && make run ARGS="gsc sync"
```

Then read the row for `donready.xyz`. Or pull from
https://search.google.com/search-console directly.

### Format

```
## YYYY-MM-DD — <one-line hypothesis or action>
- **Status:** active | testing | shipped | failed | abandoned
- **KPI:** <what GSC metric / query / page>
- **Baseline:** <numbers at start>
- **Action:** <what was done; 1-2 lines>
- **Result:** <numbers after window; "TBD — review YYYY-MM-DD" until then>
- **Learning:** <why it worked / didn't; what to try next; "TBD" until reviewed>
```

---

## 2026-05-08 — site scaffolded; growth log started
- **Status:** active
- **KPI:** any GSC traffic — clicks, impressions, indexed-page count
- **Baseline:** 0 clicks / 0 impressions (just deployed)
- **Action:** project scaffolded via `portfolio bootstrap`; first deploy
  pending. After deploy: verify in GSC as `sc-domain:donready.xyz` and submit
  the sitemap.
- **Result:** TBD — review 2026-06-05
- **Learning:** TBD

## 2026-06-27 — rewrite /figs-vs-mandala with verifiable specifics + JSON-LD (thin-content fix)
- **Status:** active
- **KPI:** indexing state of `/figs-vs-mandala/` in GSC (Crawled–currently not indexed → Indexed); secondarily impressions/clicks on "figs vs mandala" comparison queries
- **Baseline:** page crawled but **not indexed**; content judged thin/generic; ~0 impressions on brand-comparison queries
- **Action:** Replaced hedged, fabricatable prose with first-hand-quality, sourced specifics for both brands — real fabric blends (FIGS FIONx 72/21/7 vs Mandala Equa-Tek 75/19/6), pocket counts (1/6 vs 6/9), measured inseams, dated June-2026 prices ($42/$52 vs $19.99/$29.99); added sections on durability-after-washes, fluid-resistant/antimicrobial treatments, opacity, tall/petite sizing, and shipping/returns (real day counts); a cross-brand sizing table derived from both brands' published measurement charts; honest negatives for **both** brands; and an authorship/"last updated June 2026" + methodology block. Added valid FAQPage + BreadcrumbList JSON-LD and a visible breadcrumb. All source URLs logged in `docs/references.md`.
- **Result:** TBD — review 2026-07-25
- **Learning:** TBD. Hypothesis: Google's thin/helpful-content filter demotes spun-style comparison prose; replacing it with verifiable, hard-to-fabricate specifics + structured data should flip the page to Indexed. Process learnings already banked: (1) gather facts via per-brand web-research agents, mark unverifiable values `<!-- TODO: verify -->` rather than guessing, then clear TODOs with derived-from-published-data where possible (the cross-brand sizing table came from aligning both measurement charts, which turned out near-identical XS–XL — the real difference is cut, not numbers); (2) WebFetch's text scrape of `wearfigs.com/size-charts` returned hallucinated numbers — correct values came from FIGS' size-guide PDF, so verify size data from primary images/PDFs, not scraped text. If indexing improves, apply the same rewrite pattern to the other comparison/informational pages.
