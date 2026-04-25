# ux-ab-lab

Seven-agent cell that ships **10 radically different landing-page concepts** for the same product, then deploys each to its own URL on Vercel for live traffic-split testing.

Not A/B nudges. Not "same hero, different CTA color". The ten are full-spectrum design swings — different audience framings, different visual systems (palette, type, layout, motion), different narrative orderings — each defensible as its own coherent take.

## Structure (7 workspaces)

```
Design Director
├── UX Researcher            ← competitor archetypes, audience framings, mood references
├── Visual Designer          ← per-concept spec (palette / type / layout / motion)
├── React Engineer           ← /v01../v10 routes, no shared visual code
├── Deploy Engineer          ← Vercel publish, URL table, per-concept rollback
├── A11y + SEO Auditor       ← WCAG AA per concept + canonical strategy decision
└── Perf Auditor             ← Core Web Vitals per concept against per-concept baseline
```

## Env

Required: **one of**
- `ANTHROPIC_API_KEY` *(API billing)*
- `CLAUDE_CODE_OAUTH_TOKEN` *(Claude subscription — no API key needed)*

Recommended:
- `SERPER_API_KEY` — structured competitor SERP data for the researcher
- `VERCEL_TOKEN` — lets the deploy engineer push to Vercel non-interactively

## SEO strategy — read first

Two cases per concept:

- **Case A** — concepts target the same audience + same keyword cluster: pick one canonical, all others canonicalise to it with `noindex, follow`.
- **Case B** — concepts target distinct audiences/keywords (one for ops teams, one for indie devs, etc.): each is its own canonical, indexed independently.

The A11y + SEO Auditor decides per concept based on the Director's direction theses. Default to Case A when intent is shared; never use `robots.txt` disallow (blocked pages can't emit canonical headers).

## Runtime

`claude-code / sonnet` throughout. Creative + code-heavy work, reasoning quality matters.

## Import

```
github://Molecule-AI/molecule-ai-org-template-ux-ab-lab
```
