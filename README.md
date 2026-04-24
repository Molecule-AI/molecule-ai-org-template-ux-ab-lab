# ux-ab-lab

Seven-agent cell for rapid landing-page A/B variant generation on Vercel. Ship 100 variants, one hypothesis per variant, with SEO + a11y + perf gates that prevent the usual A/B traps (duplicate content, CLS regressions, token sprawl).

## Structure (7 workspaces)

```
Design Director
├── UX Researcher            ← angles, competitor teardowns, copy mining
├── Visual Designer          ← per-variant layout spec (markdown)
├── React Engineer           ← /vNNN routes, shared component library
├── Deploy Engineer          ← Vercel publish, URL table, rollback
├── A11y + SEO Auditor       ← WCAG AA + canonical/noindex gate
└── Perf Auditor             ← Core Web Vitals gate per variant
```

## Env

Required: **one of**
- `ANTHROPIC_API_KEY` *(API billing)*
- `CLAUDE_CODE_OAUTH_TOKEN` *(Claude subscription — no API key needed)*

Recommended:
- `SERPER_API_KEY` — structured SERP data for the researcher
- `VERCEL_TOKEN` — lets the deploy engineer push previews non-interactively

## SEO strategy

A/B testing 100 variants of the same page is a duplicate-content minefield for SEO. The A11y + SEO Auditor enforces:

1. One **canonical** variant; every other variant's `<link rel="canonical">` points at it.
2. `noindex, follow` on every non-canonical variant.
3. Sitemap contains ONLY the canonical URL.
4. Never `robots.txt` disallow — blocked pages can't emit canonical headers.
5. Internal links always point at the canonical URL.

## Runtime

- `claude-code / sonnet` throughout. Creative and code-heavy work, reasoning quality matters.

## Import

```
github://<your-org>/molecule-starter-template-orgs/ux-ab-lab
```
