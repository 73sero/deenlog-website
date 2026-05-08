# DeenLog Marketing Website — Design Spec

Version 2.0 · 2026-05-08 (DeenLog rebrand)

> The single source of truth is `index.html` and `privacy.html`. This file is a high-level design rationale; concrete numbers live next to the code.

---

## 1. Aesthetic Direction

**White-primary, charcoal-typed, cream-accented.** Inverts the prior dark-mode aesthetic to match the B-Light app icon (charcoal "deenlog" wordmark on near-white). Reads as quiet, premium, daily-use. Cream pulls warmth so the site doesn't feel sterile.

The app itself stays dark (it's a daily-use OLED-friendly UI). The marketing site is light. Phone mockups embed the dark app screen inside a dark `#1C1C1E` device frame — the contrast against the light page makes the screenshots pop.

---

## 2. Color Tokens

```css
:root {
  --bg:               #FFFFFF;     /* page bg */
  --bg-subtle:        #FAFAFA;     /* alternate section bg (companion section) */
  --surface:          #FFFFFF;     /* feature cards */
  --surface-warm:     #F5EFE2;     /* cream accent — feature icon bg, trust section bg */
  --surface-warm-deep:#EDE4CC;     /* deeper cream for inset / list bullets */
  --surface-charcoal: #181818;     /* CTA buttons, inverted surfaces */

  --text:             #181818;     /* primary text, h1/h2 */
  --text-secondary:   rgba(24, 24, 24, 0.62);   /* body text, taglines */
  --text-tertiary:    rgba(24, 24, 24, 0.42);   /* overlines, captions, muted labels */
  --text-muted:       rgba(24, 24, 24, 0.28);   /* separators, decorative */
  --text-on-charcoal: #FAFAFA;     /* text inside dark CTA buttons */

  --accent:           #181818;     /* CTA bg + interactive — pure charcoal */
  --accent-warm:      #8A6E3A;     /* warm gold-brown used for feature tags + list bullet rims */

  --border:           rgba(24, 24, 24, 0.10);   /* card borders, footer divider */
  --border-strong:    rgba(24, 24, 24, 0.16);   /* card hover borders */
  --border-subtle:    rgba(24, 24, 24, 0.05);   /* faint section dividers */
}
```

**Why warm cream** (`#F5EFE2`) and not pure gray neutrals: it ties to the app's `Theme.swift` cream (`#f5f0e1`) and gives the site a calmer, less corporate feel — appropriate for daily Islamic practice content.

**Why no blue/green accents:** the brand reads as monochrome (charcoal-on-white) with cream as the only color note. Adding iOS blue or success green dilutes the brand.

---

## 3. Typography

System font stack, no web fonts loaded:

```css
font-family: -apple-system, BlinkMacSystemFont, 'SF Pro Display', 'SF Pro Text', 'Helvetica Neue', Arial, sans-serif;
```

| Role | Size (desktop / mobile) | Weight | Tracking | Notes |
|---|---|---|---|---|
| Hero h1 | 56 / 36 px | 800 | -1.8 / -1.0 px | Tight, display-y |
| Section h2 | 40 / 28 px | 800 | -1.0 / -0.6 px | Same weight as h1 for unified hierarchy |
| Card h3 | 19 px | 600 | -0.2 px | Smaller than typical to keep cards quiet |
| Lead | 19 px | 400 | 0 | Subtitle / hero tagline |
| Body | 16 / 15 px | 400 | 0 | line-height 1.6 |
| Body small | 15 px | 400 | 0 | Card body |
| Overline | 11 px | 700 | +2 px, uppercase | Section labels |
| Caption | 13 px | 500 | +0.2 px | CTA notes, copyright |

The brand wordmark itself is **not** rendered as live text on the page — it's an image (`screens/app-icon.png`, derived from `docs/brand/DeenLog-4K-Light.png`). This avoids font-substitution risk on non-Apple platforms.

---

## 4. Layout

- **Container:** `max-width: 1080px`, `padding: 0 24px` (desktop), `0 20px` (mobile)
- **Container narrow:** `max-width: 760px` (used for privacy.html intro / hero copy)
- **Section vertical rhythm:** `120px` desktop, `80px` mobile
- **Card grid:** 3 cols (desktop) → 2 cols (tablet, ≤1023px) → 1 col (mobile, ≤639px)
- **Trust badges grid:** 5 cols (desktop) → 3 cols (tablet) → 2 cols (mobile)
- **Widgets section:** 2 cols (text + image, desktop) → 1 col stacked (≤1023px)

---

## 5. Components

### Hero
- Centered. Top `96px` padding (desktop) / `72px` (mobile)
- Wordmark image: 200px wide (60vw max on mobile)
- h1 + tagline + ghost CTA + small note
- Phone mockup follows below, animated in 0.25s after hero content

### Phone frame
- Width: 320 (desktop) / 280 (tablet) / 240 (mobile)
- `aspect-ratio: 9 / 19.5`
- `background: #1C1C1E` (iOS dark frame), `border-radius: 44px`, `padding: 12px`
- Drop shadow: `0 30px 80px rgba(24,24,24,0.18), 0 8px 24px rgba(24,24,24,0.08)`
- Dynamic Island pill notch (100×28, `border-radius: 14px`)
- Inner `.phone-screen` clipped to `border-radius: 34px`

### Feature card
- `padding: 28px`, `border-radius: 18px`, `border: 1px solid var(--border)`
- Hover: border darkens, lifts `-2px`, shadow appears
- Icon container: 44×44, `border-radius: 12px`, cream background

### Trust badge
- Centered text. Icon container: 52×52, white bg with border (sits on cream section)
- Label: 14/700, Description: 13/secondary

### CTA buttons
- **Solid:** charcoal bg `#181818`, off-white text, `border-radius: 14px`, padding `16px 32px`. Hover lifts `-1px` + deeper shadow.
- **Ghost** (pre-launch): same dimensions, transparent bg, charcoal-tinted border. `cursor: default` (it's a status, not a link).

---

## 6. Animations

- Hero content: 0.8s `heroFadeIn` on load (translate up 20px → 0)
- Hero phone: same animation, delayed 0.25s
- Sections: `IntersectionObserver` toggles `.visible` class. Fade in + translate up 24px → 0 over 0.6s.
- Feature card stagger inside a `.fade-in` container: nth-child delays 0/70/140/210/280/350ms
- All animations gated by `@media (prefers-reduced-motion: reduce)` — instant render when reduce-motion is on.

---

## 7. Bilingual Strategy

CSS-class toggle, no server-side i18n. Default = EN.

```html
<h1>
  <span class="en">Your deen,<br>daily tracked.</span>
  <span class="de">Dein Deen,<br>täglich getrackt.</span>
</h1>
```

- `.de { display: none; }` by default
- `<html class="lang-de">` flips `.de` to display, hides `.en`
- Block-level (`p.de`, `div.de`) uses `display: block`; inline (`span.de`, `a.de`) uses `display: inline`
- Button toggle persists choice in `localStorage('deenlog-lang')`
- Initial detection: saved pref → browser locale (`navigator.language.startsWith('de')`) → EN fallback
- Description meta tag is updated at runtime to match

---

## 8. Accessibility

- Contrast: charcoal `#181818` on `#FFFFFF` = 16.9:1 (AAA). All text colors pass AA at minimum, AAA for the primary tier.
- Focus ring: `2px solid var(--accent)` + `3px outline-offset`
- All images have descriptive `alt`
- Phone mockup: `role="img"` + `aria-label` describing the screen content
- Language toggle uses `aria-pressed` to communicate active state
- Section landmarks: `<main>`, `<header>`, `<section aria-labelledby="...">`, `<footer>`
- CTA-ghost uses `role="status"` (it's a "coming soon" state, not a link)
- `prefers-reduced-motion` honored

---

## 9. Performance

- Single HTML file, embedded `<style>` and `<script>`. No build step.
- No web fonts → zero font requests.
- Inline SVG icons.
- Largest asset: `screens/screen-widgets.png` (~760KB at 1200w). All other screenshots ~50–70KB at 640w.
- Total page weight (HTML + CSS + JS + above-fold images): ~150KB on first paint.
- `loading="lazy"` on widgets image (below fold).

---

## 10. Files

```
docs/website/
  index.html              ← landing page
  privacy.html            ← privacy policy
  COPY.md                 ← this directory's copy spec
  DESIGN-SPEC.md          ← this file
  SECURITY-AUDIT.md       ← CSP / referrer / scraper-defence audit
  screens/
    app-icon.png          ← 512×512 hero wordmark (from B-Light master)
    apple-touch-icon.png  ← 180×180 iOS home screen
    favicon-192.png       ← 192×192 standard favicon
    favicon-32.png        ← 32×32 light-mode favicon
    favicon-dark-32.png   ← 32×32 dark-mode favicon (white wordmark)
    og-preview.png        ← 1200×630 OG card
    og-preview.svg        ← OG source (rendered via rsvg-convert)
    screen-today.png      ← hero phone mockup (640w)
    screen-templates.png  ← (640w, currently unused but staged)
    screen-widgets.png    ← widgets section (1200w)
    screen-todos.png      ← (640w, currently unused but staged)
    screen-supps.png      ← (640w, currently unused but staged)
    screen-milestones.png ← (640w, currently unused but staged)
```

Non-hero screenshots are staged for future use (e.g., a feature gallery or supporting visuals on individual feature cards).

---

## 11. Deployment

GitHub Pages from `73sero/deenlog-website` repo, branch `main`, path `/`.

Live URL: `https://73sero.github.io/deenlog-website/`

Renamed from `dialed-website` (previous URL: `https://73sero.github.io/dialed-website/`) on 2026-05-08 as part of the DeenLog rebrand. GitHub provides automatic redirects for ~30 days after a rename.
