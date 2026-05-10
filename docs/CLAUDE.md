# CLAUDE.md — donready.xyz

Per-project orientation for Claude. Read this first when picking up
work on this site. Index of conventions, deferred decisions, and
non-features that aren't obvious from the code or git history.

## Project

<1-2 sentence description — fill in: what does this site do, who is
the user, what is the stack (donready.xyz runs on the sites/* workspace
shared infra: Vite or Astro + pnpm + Cloudflare Pages, with Makefile
forwarding to the central builder).>

## Commands

```bash
# Build / dev (forwards to the parent Makefile)
make deps           # install deps via the central builder
make dev            # local dev server
make build          # production build → dist/

# Test (per-stack — adjust as needed)
make test           # if a test suite is wired in

# Deploy
git push            # Cloudflare Pages auto-builds on push to main
```

## Conventions

  - Build path: this project's `Makefile` → `../Makefile` (parent
    workspace) → `~/work/projects/builder/` (central builder).
  - Stack: pnpm-only. No `package-lock.json` / `bun.lockb` / `yarn.lock`.
  - Deploy: Cloudflare Pages via `wrangler.jsonc`. No `_redirects`
    SPA fallback (uses CF's `not_found_handling` instead).

## Prompts log — when to update

After a **major change** (new route or feature, infra / deploy / stack
decision, dependency overhaul), append a dated `## YYYY-MM-DD` entry
to `docs/Prompts.md` with a **one-paragraph summary** of what shipped.

Summaries only — not file lists, not commit-by-commit detail. The point
is a scannable session-level history that future Claude sessions can
read in seconds to know *what state the project is in*, without needing
to re-read `git log`. Skip routine cleanups, typo fixes, or one-off
edits — those don't move the project forward.

## Deferred decisions

<Things deliberately *not* shipped. Append entries with rationale so
future Claude sessions don't re-propose them.>
