# Bayati for El Cajon — Website Redesign

Total redesign concept for **Osama Bayati, El Cajon City Council District 1** (2026).
Built for Via Del Web as a proposal artifact to show the candidate.

## Design direction

**"Local Civic"** — the campaign-poster ecosystem of El Cajon executed with modern
typographic rigor: yard-sign boldness, voter-guide clarity, warm paper, bilingual-ready.
Deliberately **not** the generic political template (stock-photo hero, red/blue,
vague "change" slogans).

- **Mode:** Persuade — visitor decides and acts (donate, volunteer, register, read)
- **Colors:** Civic Ink `#10233F` + Signal Amber `#F2A900` + Voter Paper `#FBF7EF`
- **Type:** Archivo Expanded (display) + Public Sans (body)
- **Content:** reused from the live site (bayati4elcajon.com), re-structured

## Files

| File | Purpose |
|---|---|
| `index.html` | Home page (hero, contrast strip, priorities, who, actions, endorsements, district lookup) |
| `issues-policy-agenda.html` | Full 8-position policy agenda, voter-guide grammar, ES/AR toggle |
| `campaign-blueprint.html` | Execution plan for the 3 top priorities (capital access, student success, term limits) |
| `my-team.html` | Team bios (Dr. Mark Kabban, Edward Kashou, supporting members) + join-the-team CTA |
| `DESIGN.md` | Formal design token spec (Google DESIGN.md format — lints clean) |
| `design-system.md` | Extended system doc: direction, tokens, components, accessibility, anti-slop |
| `src/input.css` | Tailwind v4 theme — tokens mirror DESIGN.md 1:1 |
| `assets/tailwind.css` | Compiled CSS (minified) |
| `assets/photos/` | Real images from the live campaign site (candidate portrait, yard-sign graphics) |
| `images/endorsements/` | Endorsement logos and portraits used by `endorsements.html` |
| `package.json` / `package-lock.json` | Local-only Tailwind CSS build tooling; no Node application runtime |

## Build

The published site is static HTML. The compiled `assets/tailwind.css` is committed,
so it can be opened or deployed without installing Node packages.

If you change `src/input.css` or the HTML class names, install the pinned development
dependencies once and rebuild the stylesheet:

```bash
npm ci
npm run build
```

For local stylesheet editing:

```bash
npm run dev
```

Open `index.html` directly in a browser (no server needed).

## Notes for Salem

- **Content provenance:** all copy reuses the live campaign site's text (their words,
  our structure). No fabricated claims; metrics used (25-year incumbent, ~5-in-10
  graduation rate) come directly from the site.
- **Photos:** all images pulled from the live campaign site (Playwright-rendered, since
  Google Sites lazy-loads them): Osama's professional portrait (846×1644, hero card),
  the yard-sign graphics. No fabricated imagery; initials avatars only where the
  campaign has no photo (team members).
- **Endorsements:** the live site's endorsements page is a 404 — the home page
  section reuses whatever endorsement names exist; nav links point to it.
- **Donate** links to their existing Donorbox; **volunteer** → `scheduling@...`;
  **register** → live site's voter search.
- **FPPC disclaimer** included in footer as required ("FUNDED BY OSAMA BAYATI...").
- The Shuffle-generated version (Claude Opus 5) is a generic template — kept only as
  a comparison reference. The hand-built "Local Civic" direction is the one to present.
