# Amarnath Partners — Website Handoff Document

## Project Summary

Single-page landing website for **Amarnath Partners**, a boutique strategic advisory firm headquartered in Philadelphia, PA (est. 2016). The site is built as a **single vanilla HTML file** — all CSS and JavaScript are inline. No frameworks, no build tools, no dependencies beyond two Google Fonts.

---

## File Structure

```
Amarnath Partners/
└── amarnath-partners.html    ← The entire site (HTML + CSS + JS, all inline)

Supporting research & brief (for reference only — not deployed):
├── Amarnath Partners Website Brief.md
└── Website Research for Amarnath Partners.md
```

---

## External Assets (hosted, no local copies)

| Asset | URL |
|---|---|
| **Logo (PNG, transparent bg)** | `https://assets.cdn.filesafe.space/xDxYUKgrMiPrhZew4cN6/media/69dfa784db7c222f7155c0f3.png` |
| **Hero background video (MP4)** | `https://assets.cdn.filesafe.space/xDxYUKgrMiPrhZew4cN6/media/69dfa74b06cfeed550148d8b.mp4` |

> **Logo rendering note:** A CSS `filter: brightness(0) invert(1)` is applied to the logo in both the navbar and footer since both sit on dark backgrounds. This converts the logo to pure white. If a colour version of the logo is ever needed on a light section, remove or override this filter.

---

## Design System

### Color Tokens (`CSS :root`)

| Token | Value | Usage |
|---|---|---|
| `--white` | `#f8f7f4` | Warm off-white — page background, card backgrounds |
| `--off-white` | `#f0ede8` | Slightly warmer — alternating section backgrounds |
| `--charcoal` | `#0f1114` | Deepest dark — hero bg, footer |
| `--charcoal-mid` | `#191c21` | Mid-dark — complexity section, nav drawer |
| `--navy` | `#0c1624` | Deep navy — reference token |
| `--text` | `#1a1918` | Primary body text on light backgrounds |
| `--text-2` | `#4a4744` | Secondary body text |
| `--muted` | `#6b6865` | Captions, list items, supporting text |
| `--border` | `#d5d0ca` | Standard borders |
| `--border-lt` | `#e6e2dc` | Light hairline borders |
| `--accent` | `#2b4568` | Deep steel navy — labels, rules, service card borders, dots (light sections) |
| `--accent-dim` | `rgba(255,255,255,.28)` | Dim white accent for dark section rules/lines |

> **There is no gold accent.** Gold (`#b8985a`) was intentionally removed in favour of the navy/white system above.

### Contact Section Background
The contact section uses a hardcoded `background: #0e1829` (deep navy) rather than a token — this gives it a visually distinct, lighter feel compared to the charcoal sections above it.

### Typography

| Role | Font | Weights |
|---|---|---|
| **Headings** | Playfair Display (Google Fonts) | 400 (regular), 400 italic, 500 |
| **Body / UI** | Inter (Google Fonts) | 300 (light), 400 (regular), 500 (medium) |

- Base font size: `16px`
- Heading scale: `clamp()` based, fluid from mobile to desktop
- All nav labels, section labels, buttons: uppercase, `letter-spacing: .18–.3em`, Inter

### Spacing Tokens

| Token | Value |
|---|---|
| `--pad-x` | `clamp(1.25rem, 5vw, 4rem)` — horizontal page padding |
| `--pad-y` | `clamp(4rem, 9vw, 8rem)` — vertical section padding |
| `--max-w` | `1200px` — max content width |
| `--nav-h` | `68px` — fixed nav height |

### Breakpoints

| Width | Behaviour |
|---|---|
| `≤ 767px` | Mobile: single-column layouts, hamburger nav |
| `768px–1023px` | Tablet: some 2-column grids |
| `≥ 1024px` | Desktop: full multi-column layouts |

---

## Page Sections (in order)

| # | Section | ID / Class | Background |
|---|---|---|---|
| 1 | Fixed Navigation | `.nav` | Transparent → pinned charcoal on scroll |
| 2 | Hero | `.hero` | `var(--charcoal)` + video |
| 3 | About | `#about` | `var(--white)` |
| 4 | Services | `#services` | `var(--off-white)` |
| 5 | Complexity Management | `#complexitySection` | `var(--charcoal-mid)` |
| 6 | How We Work | `#how-we-work` | `var(--white)` |
| 7 | Who We Work With | `#who-we-work-with` | `var(--off-white)` |
| 8 | Contact | `#contact` | `#0e1829` (deep navy) |
| 9 | Footer | `footer` | `var(--charcoal)` |

---

## Section-by-Section Notes

### Hero
- Full-viewport-height section with an **autoplay, muted, looping MP4** as background
- Video CSS: `filter: saturate(0.25) brightness(0.5)` — desaturated, cinematic look
- Video animation: slow zoom-out (`heroZoom`, 18s, `cubic-bezier(0.16,1,0.3,1)`) on page load
- Dark gradient overlay (`hero__overlay`) with a subtle breathing animation (`ambientDrift`, 14s loop)
- Architectural grid lines overlay (very faint white lines, `rgba(255,255,255,.025)`)
- Hero content fades in sequentially via `setTimeout` on page load (not IntersectionObserver)
- CTA: ghost-style border-only button → `#contact` anchor

### About
- 2-column grid (left: headline + stats block; right: 3 paragraphs)
- Stats block: "2016" / "PHI" — displayed large in Playfair Display

### Services
- 3-column card grid
- Each card has a `2px solid var(--accent)` top border
- Cards: 01 Go-To-Market Advisory / 02 Operational Consulting / 03 Capital Strategy & Investor Readiness
- Each card has: number, title, micro-summary (uppercase), body paragraph, bullet list

### Complexity Management (Specialized Capability)
- Dark section — `var(--charcoal-mid)`
- Contains a **live canvas particle network** (`id="complexityCanvas"`)
  - 32 nodes drifting slowly, connected by lines when within 155px
  - Colour: `rgba(185, 210, 235, opacity)` — cool blue-white
  - At rest: canvas `opacity: 0.55`
  - **On hover:** canvas fades to `opacity: 1` (1.2s CSS transition), node glow appears, lines brighten via JS lerp
  - `prefers-reduced-motion`: single static frame rendered, animation loop cancelled
- 2-column layout: left (label + heading + intro text) / right (2×2 pillar grid)
- 4 pillars: Operational Stabilization / Manufacturing Advisory / Healthcare Operations / Stakeholder & Creditor Advisory
- **Pillar hover:** background shifts to faint navy tint `rgba(43,69,104,0.18)`, text brightens

### How We Work
- 4-phase horizontal strip (Roman numerals I–IV)
- Phases separated by `1px` left-border hairlines
- Phases: Diagnostic Baseline / Strategic Architecture / Execution & Alignment / Long-Term Stewardship

### Who We Work With
- **2×2 grid** (4 cards) — not 3-column
- Cards: Founder-Led Businesses / Growth-Stage Companies / Leadership Teams in Transition / Companies Pursuing Strategic Partnerships or Expansion

### Contact
- Split 2-column: left (headline + body + email CTA + address) / right (inquiry form)
- Form submits via `mailto:` — JS constructs and opens `mailto:info@amarnathpartners.com`
- Contact email: `info@amarnathpartners.com`
- Address: 225 S 18th Street, Philadelphia, PA

### Footer
- Dark charcoal background
- Logo (white filter, 35% opacity)
- Legal disclaimer
- Privacy Policy + Terms of Use links (placeholder `#` hrefs — need real URLs)
- Copyright: © 2026 Amarnath Partners

---

## JavaScript Features

| Feature | Implementation |
|---|---|
| Nav pin on scroll | `window.addEventListener('scroll')` — adds `.pinned` class after 70px |
| Mobile drawer | Toggle `.open` on `#drawer`, `aria-expanded` managed |
| Scroll-to-top button | Fixed bottom-left, appears after 400px scroll, `window.scrollTo({ behavior: 'smooth' })` |
| Scroll reveal animations | `IntersectionObserver` — adds `.visible` to `.reveal` elements (threshold 0.1) |
| Hero reveal | `setTimeout` cascade (180ms base, +140ms per element) — bypasses IntersectionObserver |
| Particle network | IIFE canvas animation in the Complexity section (see notes above) |
| Contact form | `form#inquiry-form` → `preventDefault` → constructs `mailto:` URL |

---

## Animation System

### Scroll Reveal Classes

| Class | Delay |
|---|---|
| `.reveal` | 0s |
| `.reveal-d1` | 0.12s |
| `.reveal-d2` | 0.24s |
| `.reveal-d3` | 0.36s |
| `.reveal-d4` | 0.48s |

- Easing: `cubic-bezier(0.16, 1, 0.3, 1)` — expo-out (premium feel)
- Duration: `0.9s`
- Starting transform: `translateY(32px)`
- `prefers-reduced-motion`: all animations/transitions set to `0.01ms`

---

## Design Inspiration / Reference Sites

Per the client brief:
- [Centerview Partners](https://www.centerviewpartners.com/) — monolith minimalism
- [Qatalyst Partners](https://qatalyst.com/) — cinematic hero
- [PJT Partners](https://www.pjtpartners.com/) — modern flow
- [Golub Capital](https://golubcapital.com/) — "Good Boring" tone
- [Lazard](https://www.lazard.com/) — institutional authority

---

## Tone & Copy Guidelines

- **Avoid:** "passionate," "innovative," "world-class," "cutting-edge"
- **Use:** Execute, Restructure, Optimize, Align, Stabilize, Clarify
- Reading level: 8th grade (Hemingway-style)
- Voice: senior-led, direct, institutional — not warm/startup
- Headlines: benefit-driven, 6–12 words max
- All CTAs: ghost-style border-only buttons on dark backgrounds

---

## Known Items / Future Work

| Item | Notes |
|---|---|
| **Privacy Policy & Terms** | Footer links point to `#` — real legal pages need to be added |
| **Contact form backend** | Currently `mailto:` only. For production: connect to Formspree, EmailJS, or a server-side handler |
| **OG image** | No `og:image` meta tag yet — add a 1200×630px brand image |
| **Favicon** | No favicon set — add `<link rel="icon">` |
| **Canonical URL** | Set to `https://amarnathpartners.com/` — confirm domain is correct |
| **Font duplication** | Google Fonts URL has `&display=swap` twice — harmless but can be cleaned up |
| **Analytics** | No tracking script installed — add GA4 or equivalent before launch |
| **Hosting** | Site is a single HTML file — can be deployed directly to Netlify, Vercel, GitHub Pages, or any static host |

---

## Quick-Edit Cheat Sheet

| What to change | Where to look |
|---|---|
| Logo image | Search `nav__logo-img` (navbar) and `footer__brand img` (footer) |
| Hero video | Search `hero__video` → `<source src=` |
| Hero tagline | Search `hero__h1` |
| Contact email | Search `info@amarnathpartners.com` (appears in HTML + JS) |
| Address | Search `225 S 18th` |
| All accent colour | Change `--accent: #2b4568` in `:root` |
| Section order | Sections are in sequence inside `<main>` — cut/paste to reorder |
| Add a new section | Copy an existing `.section` block, assign a new `id`, add a nav `<li>` link |
| Particle network | IIFE at the bottom of `<script>` — edit `NODE_COUNT`, `MAX_DIST`, `BASE_SPEED`, `HUE` |
