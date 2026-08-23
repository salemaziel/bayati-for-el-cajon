# Design System — Bayati for El Cajon

**Project:** Bayati for El Cajon — City Council District 1 campaign website (redesign)
**Scope:** index (home) + issues-policy-agenda · candidate: Osama Bayati · 2026
**Design direction:** "Local Civic" — the campaign-poster ecosystem of El Cajon, executed with modern typographic rigor.

---

## 1. Design Direction

### The world
The cultural home is the **local civic campaign**: yard signs, precinct voter guides, bilingual flyers at the swap meet, the district map on the kitchen table. Not the national-political stock-photo template (flag-waving hero, red/blue gradient, vague "change" slogan) — the *physical* local campaign, which has its own honest visual grammar: high-contrast signage, numbered policy positions, real names, real proof.

The site should feel like the best yard sign in District 1 got a website: bold condensed display type you can read from a car window, warm optimistic color, and voter-guide clarity for policy.

### Mode
**Persuade.** The visitor must quickly understand: (1) who is running, (2) against what, (3) what he will do, (4) what to do next — donate, volunteer, register, read the agenda.

### What it refuses
- Generic political template (hero stock photo + flags + red/blue gradient + "change" platitudes)
- AI-design slop: tech gradients, indigo default accent, feature-tile grids with icon toppers, glassmorphism, monument stats
- The incumbent's visual language entirely (the old site is anti-reference)

### Signature elements
1. **Condensed campaign-poster display type** — Archivo Expanded Black for headlines, tight tracking, ALL-CAPS kicks
2. **Signal amber + navy ink + warm paper** — Committed palette; amber carries 30–60% of surface
3. **Numbered policy positions** styled like a voter guide — big numerals, clear hierarchies
4. **Bilingual-ready** — ES/AR toggle affordance in nav (the original site has Spanish and Arabic versions of Issues)
5. **Honest proof** — endorsements with real names/titles, live PRE-style evidence, district map link
6. **FPPC disclaimer** — "FUNDED BY OSAMA BAYATI, FOR CITY COUNCIL" in the footer, as required

---

## 2. Color

### Strategy: Committed

One saturated accent (Signal Amber) carries 30–60% of the surface. Navy provides gravity; paper provides warmth.

| Token | Value | Role |
|---|---|---|
| `--c-ink` | `#10233F` | Primary text, dark surfaces, navy fields |
| `--c-ink-2` | `#1D3557` | Secondary navy (section fields, hovers) |
| `--c-amber` | `#F2A900` | Primary accent — CTAs, highlights, numerals, rules |
| `--c-amber-deep` | `#D98E00` | Amber hover / pressed |
| `--c-paper` | `#FBF7EF` | Warm background (voter-guide paper) |
| `--c-white` | `#FFFFFF` | Cards, light surfaces |
| `--c-mist` | `#EDE8DC` | Paper-darkened borders, dividers on paper |
| `--c-slate` | `#5A6B82` | Muted secondary text on light |
| `--c-fog` | `#9FB0C6` | Muted text on navy (borders on navy) |
| `--c-good` | `#1E7A46` | Success / "verified" states |

### Contrast (WCAG AA)
- Ink on paper: `#10233F` on `#FBF7EF` — **14.9:1** ✓
- White on navy: `#FFFFFF` on `#10233F` — **14.3:1** ✓
- Amber on ink: `#F2A900` on `#10233F` — **9.5:1** ✓ (large text/CTA labels)
- White on amber (primary button): `#FFFFFF` on `#F2A900` — **2.5:1** — **does NOT pass for text** → primary buttons use **ink text on amber** (`#10233F` on `#F2A900` = 9.5:1 ✓). White-on-amber reserved for non-text accents.
- Slate on paper: `#5A6B82` on `#FBF7EF` — **5.4:1** ✓

**Rule: ink-on-amber for CTA labels; never white text on amber.**

---

## 3. Typography

### Fonts
- **Display:** Archivo (Expanded, weights 500–800). Google Fonts. Condensed feel for campaign-poster energy.
- **Body:** Public Sans (400/600/700). The US civic face — clean, humanist, government-trustworthy. Google Fonts.

### Type scale (desktop)

| Token | Font | Size / line-height | Weight | Tracking | Use |
|---|---|---|---|---|---|
| `display-xl` | Archivo Expanded | `clamp(3rem, 7vw, 5.5rem)` / 1.02 | 800 | `-0.01em` | Hero statement |
| `display-lg` | Archivo Expanded | `clamp(2.25rem, 4.5vw, 3.5rem)` / 1.05 | 800 | `-0.01em` | Section headers |
| `display-md` | Archivo Expanded | `clamp(1.5rem, 2.5vw, 2rem)` / 1.15 | 700 | `-0.01em` | Card titles, sub-hero |
| `kicker` | Archivo Expanded | `0.8125rem` / 1.4 | 700 | `0.14em` | ALL-CAPS section kickers |
| `body-lg` | Public Sans | `1.125rem` / 1.65 | 400 | — | Lead paragraphs |
| `body` | Public Sans | `1rem` / 1.6 | 400 | — | Standard text |
| `body-sm` | Public Sans | `0.9375rem` / 1.55 | 400 | — | Secondary text |
| `label` | Public Sans | `0.875rem` / 1.4 | 600 | `0.02em` | Buttons, form labels, meta |

Mobile: display-xl scales via clamp; body stays 1rem+ (never below 16px for comfort).

---

## 4. Spacing & Layout

### Grid
- **12-column** desktop grid, max-width **1200px** container (`--container`).
- Gutter: `24px` desktop / `16px` mobile.
- Section padding: `clamp(4rem, 9vw, 7.5rem)` vertical rhythm — generous, editorial.

### Space scale (4px base)

| Token | Value |
|---|---|
| `--sp-1` | 4px |
| `--sp-2` | 8px |
| `--sp-3` | 12px |
| `--sp-4` | 16px |
| `--sp-5` | 24px |
| `--sp-6` | 32px |
| `--sp-7` | 48px |
| `--sp-8` | 64px |
| `--sp-9` | 96px |
| `--sp-10` | 128px |

### Rhythm rule
More space above a heading than below it. Sections alternate density (dense passage earns a quiet one).

---

## 5. Shape & Elevation

- **Radii:** `--r-sm: 4px`, `--r-md: 8px`, `--r-lg: 12px` — modest, civic (not pill/not bubbly).
- **Buttons:** `--r-sm` (4px) — squared, signage-like.
- **Cards:** `--r-md` (8px).
- **Shadows:** restrained. `--shadow-1: 0 1px 2px rgba(16,35,63,.08)`, `--shadow-2: 0 8px 24px rgba(16,35,63,.12)`. Elevation via color fields (navy blocks, amber rules) more than shadows.

---

## 6. Components

### Buttons
- **Primary:** amber field, ink text, `--r-sm`, weight 700, `padding: 14px 24px`. Hover: amber-deep, translateY(-1px). Focus ring: 2px ink offset 2px.
- **Secondary:** transparent, 2px ink border, ink text. Hover: ink field, white text.
- **On-navy:** white field/ink text; or amber/ink. Ghost on navy: 2px white border.
- Min height 44px (touch target).

### Nav
- Sticky top, paper/white, hairline bottom border. Logo wordmark left ("BAYATI for El Cajon" — Archivo Expanded, ink, amber period). Links right (Public Sans 600, 15px, ink, amber underline on hover/active). Mobile: hamburger → full overlay panel (navy field, white links, amber active).
- Donate button is always visible — the primary action.

### Policy cards (Issues page)
Voter-guide grammar: large numeral (amber, Archivo Expanded), kicker category, Archivo title, body copy, optional "reads like" evidence. Numbered 1–8. Card: white on paper, 1px mist border, radius 8, generous padding. Hover: 2px amber left rule + shadow-2.

### Endorsement tiles
Name + title, quote or context line. Avatar initial in navy circle with amber initial (no fake photos).

### Team cards
Name, role kicker, bio. Initial avatar. No fake headshots — real photos slot in.

### Footer
Navy field. Wordmark, quick links, contact (`@bayati4elcajon.com`, (619) 484-6327), social placeholders, **FPPC disclaimer** ("FUNDED BY OSAMA BAYATI, FOR CITY COUNCIL"), "Paid for by Bayati for El Cajon City Council 2026".

### Forms (volunteer/register)
Public Sans, ink labels, 1px ink border inputs, focus ring amber, min 44px, clear error states.

---

## 7. Motion

- **Posture:** civic, confident, restrained. No loops, no gimmicks.
- Hero: staggered reveal (kicker → headline → copy → CTAs) with 300–500ms ease-out, translateY(12px)→0, opacity 0→1. Respect `prefers-reduced-motion` (disable).
- Hover: buttons lift 1px, links get amber underline sweep.
- Policy numbers: subtle count-up optional — skip by default (restraint).
- Nav overlay: fade + slight slide, 200ms.

---

## 8. Imagery

- Real candidate photography slots in (navy/amber treatment). Placeholders are typographic/initial-based — **no fake stock photos, no AI portraits**.
- Hero: full-bleed navy field with bold typographic statement; candidate portrait in a right-hand slot (real photo to be supplied).
- District map: link to the live voter lookup (`https://www.bayati4elcajon.com/` district search) — honest utility, not a fake map.

---

## 9. Accessibility

- WCAG 2.2 AA: contrast table above; focus-visible rings everywhere; semantic HTML (header/nav/main/section/footer); skip-to-content link; 44px min touch targets; `prefers-reduced-motion` respected; lang attributes; alt text on all imagery.
- Bilingual-ready: ES/AR toggle in nav (content slots wired, translations to be supplied by campaign).

---

## 10. Anti-slop checklist (applied)

- [x] No tech gradient (navy fields + solid amber)
- [x] No default indigo accent (deliberate amber, chosen for optimism + yard-sign tradition)
- [x] No equal-weight feature-tile grid (hero is a statement; policies are numbered, prioritized)
- [x] No accent rails on cards (amber left rule only on hover state, not resting decoration)
- [x] No glassmorphism
- [x] No monument stats (real numbers only where true: 25-year incumbent, ~5-in-10 grad rate, both from the site)
- [x] No icon-topper tiles (typographic system)
- [x] Composition committed per surface (Decide/Learn: hero + statement + numbered proof)
- [x] Type chosen with intent (Archivo Expanded + Public Sans — not Inter/system default)
- [x] Surface correct: Persuade → Decide/Learn composition
