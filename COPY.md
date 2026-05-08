# DeenLog Website Copy

Marketing copy for the DeenLog landing page (`index.html`). Single-page site, bilingual EN/DE, white-primary aesthetic. Audience: Muslim users wanting a private daily-practice tracker on iOS.

> The source-of-truth is `index.html` itself. This file documents intent and the prose blocks; if anything diverges, the HTML wins.

---

## Positioning

DeenLog is a **private iOS app for daily Islamic practice** — Salah, Adhkar, Dhikr, Quran, Tahajjud, Sunnah fasting — alongside supplements, habits, and todos. Local-first, no account, no ads, no tracking.

Brand etymology: **Deen** (دين, way of life) + **Log** (English, daily journal). Hybrid Arabic-English compound, lowercase wordmark.

---

## Page Structure

| # | Section | Purpose |
|---|---------|---------|
| 1 | **Hero** | Wordmark, headline, tagline, App Store CTA, phone mockup |
| 2 | **Daily Practice** (pillar) | 6 cards: Salah, Adhkar, Dhikr, Quran, Tahajjud, Sunnah Fasting |
| 3 | **And the rest of your day** (companion) | 3 cards: Supplements, Habits, Todos |
| 4 | **Home Screen / Widgets** | 9 widgets, screenshot-driven |
| 5 | **Privacy by default** | 5 trust badges |
| 6 | **Final CTA** | App Store call-to-action |
| 7 | **Footer** | Privacy, contact, copyright |

---

## Hero

### Headline
- EN: **Your deen, daily tracked.**
- DE: **Dein Deen, täglich getrackt.**

### Tagline
- EN: A private iOS app for Salah, Adhkar, Dhikr, Quran and Tahajjud — alongside your supplements, habits, and todos.
- DE: Eine private iOS-App für Salah, Adhkar, Dhikr, Quran und Tahajjud — mit deinen Supplements, Habits und Todos.

### CTA
- Primary state (pre-launch): **Coming soon on the App Store** / **Bald im App Store**
- Live state (post-launch): **Download on the App Store** / **Im App Store laden**, link to `apps.apple.com/app/deenlog/idXXXXXXXXXX`
- Sub-line: Free. No account. No tracking. / Kostenlos. Kein Account. Kein Tracking.

---

## Section 2 — Daily Practice (the 6 pillars)

Section overline: **Daily practice** / **Tägliche Praxis**
Heading: **Your deen, in one place.** / **Dein Deen, an einem Ort.**

| # | Title (EN/DE) | Body |
|---|---|---|
| 1 | **Salah & Shuruq** / **Salah & Schuruq** | Prayer times for your location or your chosen mosque, with Shuruq so you never miss the Fajr window. Quiet notifications by salah name. |
| 2 | **Adhkar** | Adhkar al-Sabah and al-Masaa as guided morning and evening flows. Tap to count, swipe to advance, finish in minutes. |
| 3 | **Dhikr Counter** / **Dhikr-Counter** | A digital tasbih on your home screen. Tap the widget from the lock screen — the count syncs back into the app. |
| 4 | **Quran Khatm** / **Quran-Khatm** | Pages-per-day or juz-per-day target with a cumulative khatm counter. The number on your card is the total pages, not just today. |
| 5 | **Tahajjud** | A separate alarm for the last third of the night, anchored to your Fajr time. Wake up to qiyam, not to a notification storm. |
| 6 | **Sunnah Fasting** / **Sunnah-Fasten** | Pre-built patterns for Mondays & Thursdays, the Ayyam al-Bid (13–15 of each Hijri month), and Dawud's fast. |

---

## Section 3 — Companion (supplements, habits, todos)

Section overline: **And the rest of your day** / **Und der Rest deines Tages**
Heading: **Built for your whole life, not just one corner of it.** / **Gebaut für dein ganzes Leben, nicht nur eine Ecke.**

| # | Title | Body |
|---|---|---|
| 1 | **Supplements** | Set the schedule once — dose, timing, reminder. Tap to log. Streaks at 7, 30, 66, 100 and 365 days. |
| 2 | **Habits** | Daily, weekly, or plan-based (gym splits). Abstinence tracker with a running day count. Progress rings and weekly dots. |
| 3 | **Todos** | Labels, notes, location-based reminders, calendar export. The everyday list, without the bloat. |

---

## Section 4 — Home Screen / Widgets

Section overline: **Home screen** / **Homescreen**
Heading: **Deen at a glance.** / **Deen auf einen Blick.**

Body:
- EN: Nine widgets across three sizes. Tap your Dhikr counter from the lock screen. Watch your next salah count down. See your khatm progress on the medium card.
- DE: Neun Widgets in drei Größen. Tap deinen Dhikr-Counter vom Sperrbildschirm. Sieh den Countdown bis zur nächsten Salah. Verfolge deinen Khatm-Fortschritt auf der mittleren Karte.

Bullet list (EN / DE):
- **Dhikr counter** — interactive, tap to increment / **Dhikr-Counter** — interaktiv, Tap zählt
- **Next prayer** — with countdown, on small & medium / **Nächstes Gebet** — mit Countdown, klein & mittel
- **Today's habits** — large widget, scrollable / **Heutige Habits** — großes Widget, scrollbar
- **Hijri date** — tiny widget, set-it-and-forget-it / **Hijri-Datum** — winziges Widget, einmal anpinnen
- **Next supplement** — never miss a dose / **Nächstes Supp** — verpass keine Dosis

Visual: `screens/screen-widgets.png` (1200w from `docs/appstore/screenshots/iphone-67-original/03-widgets.png`).

---

## Section 5 — Privacy / Trust

Section overline: **Privacy by default** / **Privatsphäre by default**
Heading: **Your 'ibadah is yours. So is your data.** / **Deine 'Ibadah ist deine. Deine Daten auch.**

5 badges:

| Label EN | Label DE | Description EN | Description DE |
|---|---|---|---|
| Local-First | Local-First | Tracking data stays on your device | Trackingdaten bleiben auf deinem Gerät |
| No Account | Kein Account | Nothing to sign up for | Nichts zum Registrieren |
| No Tracking | Kein Tracking | No analytics, no ad SDKs | Keine Analyse, keine Werbe-SDKs |
| No Ads, Ever | Keine Werbung | No ads, no upsells, no nag | Keine Anzeigen, kein Upsell, kein Nerven |
| Backup & Restore | Backup & Restore | Export and import your data anytime | Daten jederzeit exportieren und importieren |

---

## Section 6 — Final CTA

Heading:
- EN: **Start logging your deen.**
- DE: **Fang an, deinen Deen zu tracken.**

Lead:
- EN: Free on the App Store. No account, no ads, no tracking.
- DE: Kostenlos im App Store. Kein Account, keine Werbung, kein Tracking.

CTA: same as hero (pre-launch ghost, post-launch live link).

---

## Footer

Brand line: **DeenLog**

Links:
- Privacy Policy / Datenschutz → `privacy.html`
- Contact / Kontakt → `mailto:serdar.saglam01@icloud.com` (assembled at runtime to defeat scrapers)

Copyright: © 2026 Serdar Saglam. All rights reserved. / © 2026 Serdar Saglam. Alle Rechte vorbehalten.

---

## Meta Tags

### EN
- **Title:** DeenLog — Your deen, daily tracked.
- **Description:** DeenLog is a private iOS app for daily Islamic practice — Salah, Adhkar, Dhikr, Quran, Tahajjud, Sunnah fasting — alongside supplements, habits, and todos. Local-first, no account, no ads.
- **OG Title:** DeenLog — Your deen, daily tracked.
- **OG Description:** A private iOS app for daily Islamic practice — Salah, Adhkar, Dhikr, Quran, Tahajjud, Sunnah fasting — plus supplements, habits, and todos.
- **OG Image Alt:** DeenLog — Your deen, daily tracked. A private iOS app for Salah, Adhkar, Dhikr, Quran, and Tahajjud.

### DE
- **Title:** DeenLog — Dein Deen, täglich getrackt.
- **Description:** DeenLog ist eine private iOS-App für tägliche islamische Praxis — Salah, Adhkar, Dhikr, Quran, Tahajjud, Sunnah-Fasten — zusammen mit Supplements, Habits und Todos. Local-first, kein Account, keine Werbung.

The `<meta name="description">` tag is updated at runtime by the language toggle JS.

---

## Implementation Notes

- **Language toggle:** EN/DE button top-right, persists choice via `localStorage('deenlog-lang')`. Defaults to browser locale, falls back to EN.
- **App Store badge:** Currently in "Coming Soon" ghost state. Two TODO comments mark the swap-in points (hero + final CTA) for when the App Store ID is assigned. Replace `idXXXXXXXXXX` with the real ID and uncomment the live `<a class="cta-button">` block.
- **Typography:** SF Pro stack (`-apple-system, BlinkMacSystemFont, 'SF Pro Display', 'SF Pro Text', 'Helvetica Neue', Arial, sans-serif`).
- **Wordmark:** The hero uses `screens/app-icon.png` (resized from `docs/brand/DeenLog-4K-Light.png`). The wordmark master is the source-of-truth for all logo placements.
- **Screenshots:** Pulled from `docs/appstore/screenshots/iphone-67-original/` (raw, uncaptioned) — the captioned `iphone-67/` versions are App Store assets and have marketing text that would clash with the website's own copy.
