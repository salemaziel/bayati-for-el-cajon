---
version: alpha
name: Bayati for El Cajon
description: Local civic campaign redesign — campaign-poster typographic energy, navy ink and signal amber on warm voter-guide paper, numbered policy positions, bilingual-ready.
colors:
  primary: "#10233F"
  secondary: "#1D3557"
  tertiary: "#F2A900"
  neutral: "#FBF7EF"
  white: "#FFFFFF"
  mist: "#EDE8DC"
  slate: "#5A6B82"
  fog: "#9FB0C6"
  good: "#1E7A46"
  amber-deep: "#D98E00"
typography:
  display-xl:
    fontFamily: "Archivo Expanded"
    fontSize: 5.5rem
    fontWeight: 800
    lineHeight: 1.02
    letterSpacing: "-0.01em"
  display-lg:
    fontFamily: "Archivo Expanded"
    fontSize: 3.5rem
    fontWeight: 800
    lineHeight: 1.05
    letterSpacing: "-0.01em"
  display-md:
    fontFamily: "Archivo Expanded"
    fontSize: 2rem
    fontWeight: 700
    lineHeight: 1.15
    letterSpacing: "-0.01em"
  kicker:
    fontFamily: "Archivo Expanded"
    fontSize: 0.8125rem
    fontWeight: 700
    lineHeight: 1.4
    letterSpacing: "0.14em"
  body-lg:
    fontFamily: "Public Sans"
    fontSize: 1.125rem
    fontWeight: 400
    lineHeight: 1.65
  body:
    fontFamily: "Public Sans"
    fontSize: 1rem
    fontWeight: 400
    lineHeight: 1.6
  body-sm:
    fontFamily: "Public Sans"
    fontSize: 0.9375rem
    fontWeight: 400
    lineHeight: 1.55
  label:
    fontFamily: "Public Sans"
    fontSize: 0.875rem
    fontWeight: 600
    lineHeight: 1.4
    letterSpacing: "0.02em"
rounded:
  sm: 4px
  md: 8px
  lg: 12px
spacing:
  sm: 8px
  md: 16px
  lg: 24px
  xl: 48px
  xxl: 96px
components:
  button-primary:
    backgroundColor: "{colors.tertiary}"
    textColor: "{colors.primary}"
    typography: "{typography.label}"
    rounded: "{rounded.sm}"
    padding: 14px
    height: 48px
  button-primary-hover:
    backgroundColor: "{colors.amber-deep}"
    textColor: "{colors.primary}"
  button-secondary:
    backgroundColor: "{colors.neutral}"
    textColor: "{colors.primary}"
    typography: "{typography.label}"
    rounded: "{rounded.sm}"
    padding: 14px
    height: 48px
  button-secondary-hover:
    backgroundColor: "{colors.primary}"
    textColor: "#FFFFFF"
  nav-link:
    textColor: "{colors.primary}"
    typography: "{typography.label}"
  policy-card:
    backgroundColor: "{colors.white}"
    textColor: "{colors.primary}"
    rounded: "{rounded.md}"
    padding: 24px
  policy-card-hover:
    backgroundColor: "{colors.mist}"
    textColor: "{colors.primary}"
    rounded: "{rounded.md}"
    padding: 24px
  footer-surface:
    backgroundColor: "{colors.primary}"
    textColor: "#FFFFFF"
  input:
    backgroundColor: "{colors.white}"
    textColor: "{colors.primary}"
    rounded: "{rounded.sm}"
    padding: 12px
---

# Bayati for El Cajon

## Overview

Osama Bayati is running for El Cajon City Council District 1 on a "next generation"
platform: youth success, term limits, small business support, senior fraud protection,
Flock camera oversight, housing affordability. The site redesign speaks in the visual
grammar of the local campaign — yard signs, voter guides, precinct flyers — executed
with modern typographic confidence. Energetic, credible, civic, youth-forward; never
the generic political template.

Primary action on every viewport: **Donate** (Donorbox). Secondary: volunteer,
register to vote, read the policy agenda.

## Colors

- **Primary (#10233F) "Civic Ink":** headline text, dark fields, footer, nav links on paper.
- **Secondary (#1D3557):** deep-navy section fields, hover states, gradient-free depth.
- **Tertiary (#F2A900) "Signal Amber":** the campaign's energy — CTAs, policy numerals,
  kicker accents, rules, highlights. Carries 30–60% of surface (Committed strategy).
- **Neutral (#FBF7EF) "Voter Paper":** warm page background, like a voter guide printed
  on cream stock.
- **White (#FFFFFF):** cards and light surfaces on paper.
- **Mist (#EDE8DC):** borders/dividers on paper.
- **Slate (#5A6B82):** muted secondary text on light surfaces.
- **Fog (#9FB0C6):** muted text and hairlines on navy.
- **Good (#1E7A46):** success / verified states.
- **Amber-deep (#D98E00):** amber hover / pressed.

Contrast: primary-on-neutral 14.9:1 · white-on-primary 14.3:1 · primary-on-tertiary
9.5:1 · tertiary-on-primary 9.5:1. **Rule: ink-on-amber for CTA labels — never white
text on amber** (2.5:1 fails AA).

## Typography

- **Archivo Expanded** — display face. Heavy weights (700/800) in ALL-CAPS kicks and
  condensed-expanded headlines. Campaign-poster energy: readable from a car window.
- **Public Sans** — body face. The US government's civic typeface: clean, humanist,
  trustworthy for policy text and forms.

Scale: display-xl clamp(3rem→5.5rem) for the hero statement; display-lg for section
headers; display-md for card titles; kicker (12px, +0.14em tracking, ALL-CAPS) above
sections; body-lg for leads; body 16px floor; label for buttons/meta.

## Layout & Spacing

12-column grid, 1200px max container, 24px/16px gutters. Section padding
clamp(4rem→7.5rem). 4px-based space scale (sm 8 / md 16 / lg 24 / xl 48 / xxl 96).
More space above headings than below. Sections alternate density. Secondary buttons
carry a 2px ink border; policy cards gain a 4px amber left rule and a soft shadow on
hover; inputs use a 1px ink border — these are documented in design-system.md.

## Elevation & Depth

Restrained. `shadow-1: 0 1px 2px rgba(16,35,63,.08)`; `shadow-2: 0 8px 24px rgba(16,35,63,.12)`.
Depth is carried by color fields (navy blocks, amber rules) more than shadows.

## Shapes

Radii are modest and civic: sm 4px (buttons), md 8px (cards), lg 12px (large surfaces).
No pills, no bubbles.

## Components

- **button-primary:** amber field, ink text, 4px radius, 48px height, weight 600.
  Hover: amber-deep. Focus ring: 2px ink, 2px offset.
- **button-secondary:** paper field, ink text, 2px ink border. Hover: ink field, white text.
- **Nav:** sticky paper bar, hairline bottom border. Wordmark "BAYATI for El Cajon"
  (Archivo Expanded, ink, amber period). Public Sans links with amber underline on
  hover/active. Donate always visible. Mobile: navy full-overlay menu.
- **Policy cards:** white on paper, 1px mist border, 8px radius, 24px padding. Amber
  numeral, kicker category, Archivo title, body copy. Hover: mist fill + 4px amber
  left rule + shadow-2.
- **Endorsement / team tiles:** real names + titles, initial avatars (navy circle,
  amber initial). No fake headshots.
- **Footer:** navy field, white text, wordmark, quick links, contact, FPPC disclaimer
  ("FUNDED BY OSAMA BAYATI, FOR CITY COUNCIL"), social placeholders.
- **Forms:** Public Sans, ink labels, 1px ink border, amber focus, 44px min targets.

## Do's and Don'ts

**Do:**
- Use amber to make *one* thing per viewport unmissable (the primary action).
- Number policies like a voter guide — big amber numerals, clear hierarchies.
- Keep paper warm and text high-contrast; the site should feel printed and civic.
- Design bilingual-first: ES/AR toggle lives in the nav.
- Keep every claim real: only facts from the campaign (25-year incumbent, grad rates,
  endorsements with names).

**Don't:**
- Don't put white text on amber (fails AA). Ink on amber always.
- Don't use red/blue party-template colors or flag imagery.
- Don't do glassmorphism, tech gradients, or an indigo default accent.
- Don't use Inter/system default typography — Archivo Expanded + Public Sans only.
- Don't fake imagery: no stock-photo heroes, no AI portraits, no fake endorsements.
- Don't equal-weight a feature-tile grid; the hero is a statement, policies are numbered.
- Don't drop the FPPC disclaimer from the footer — it is legally required.
