# Security Audit Report -- DeenLog Marketing Website

**Auditor:** Claude (automated static review)
**Date:** 2026-04-08 (revalidated 2026-05-08 post-DeenLog rebrand)
**Scope:** `docs/website/index.html`, `docs/website/privacy.html`
**Deployment target:** GitHub Pages (static, no server)

---

## 1. Sensitive Data Exposure

**Verdict: PASS (with one P1 note)**

| Check | Result |
|---|---|
| API keys / tokens / secrets | None found |
| Internal paths / server info / debug data | None found |
| GitHub repo structure leaking internal info | None found |
| Email address exposure | See issue 1.1 below |

### Issue 1.1 -- Plaintext mailto: links (P1)

**Files and lines:**
- `index.html` lines 793-794
- `privacy.html` lines 325, 365, 376-377

The email address `serdar.saglam01@icloud.com` appears in plaintext `mailto:` links in six places across both files. Spam bots routinely scrape `mailto:` hrefs.

**Recommended fix:** Light JS obfuscation. Replace every `mailto:` link with a data-attribute pattern and decode on click. Example for `index.html` footer:

```html
<!-- Replace this: -->
<a href="mailto:serdar.saglam01@icloud.com" data-lang="en">Contact</a>

<!-- With this: -->
<a href="#" class="email-link" data-u="serdar.saglam01" data-d="icloud.com" data-lang="en">Contact</a>
```

Then add at the top of the existing `<script>` block (inside the IIFE):

```js
// ── Email obfuscation ──
document.querySelectorAll('.email-link').forEach(function (el) {
  el.addEventListener('click', function (e) {
    e.preventDefault();
    var addr = el.getAttribute('data-u') + '@' + el.getAttribute('data-d');
    window.location.href = 'mailto:' + addr;
  });
});
```

This is not bulletproof against determined scrapers, but it defeats the vast majority of automated harvesting. A `noscript` fallback is not needed because users who disable JS cannot send email from a link anyway.

**Priority: P1** -- Should fix before deploy. Low effort, real spam-reduction benefit.

### Issue 1.2 -- Placeholder App Store URL (P2)

**Files and lines:**
- `index.html` lines 635, 778

The CTA links point to `https://apps.apple.com/app/deenlog/idXXXXXXXXXX`. This is a non-functional placeholder. It is not a security issue, but deploying it would send users to a dead URL.

There is also a commented-out duplicate block (lines 628-634, 771-777) that will need cleanup.

**Priority: P2** -- Replace with real ID before launch, or hide the CTA entirely until the app is live.

---

## 2. Security Headers (Meta Tags)

**Verdict: FAIL**

GitHub Pages sets a limited set of server-side headers. For static sites, meta-tag equivalents provide defence-in-depth for the CSP and referrer policy.

### Issue 2.1 -- Missing Content-Security-Policy meta tag (P1)

Neither file contains a `<meta http-equiv="Content-Security-Policy">` tag.

**Recommended fix -- add to both files immediately after `<meta charset="UTF-8">`:**

```html
<meta http-equiv="Content-Security-Policy"
      content="default-src 'none'; style-src 'unsafe-inline'; img-src 'self' data:; script-src 'unsafe-inline'; form-action 'none'; base-uri 'none'; frame-ancestors 'none';">
```

Breakdown:
- `default-src 'none'` -- deny everything by default
- `style-src 'unsafe-inline'` -- required because styles are inline
- `img-src 'self' data:` -- allows local images and the data-URI favicon
- `script-src 'unsafe-inline'` -- required because scripts are inline (no external JS)
- `form-action 'none'` -- no forms exist, block form submissions
- `base-uri 'none'` -- prevent `<base>` tag injection
- `frame-ancestors 'none'` -- prevent clickjacking (equivalent to X-Frame-Options DENY)

**Priority: P1** -- Should fix before deploy. Prevents future regressions if someone adds an external script or image.

### Issue 2.2 -- Missing Referrer-Policy meta tag (P1)

No referrer policy is set. The browser default (`strict-origin-when-cross-origin`) is acceptable, but an explicit declaration is better practice, especially given the `mailto:` links and the App Store outbound link.

**Recommended fix -- add to both files in `<head>`:**

```html
<meta name="referrer" content="strict-origin-when-cross-origin">
```

**Priority: P1** -- Trivial to add, explicit is better than implicit.

### Issue 2.3 -- No X-Content-Type-Options equivalent (P2)

`X-Content-Type-Options: nosniff` is a server-side header; there is no meta-tag equivalent. GitHub Pages does set this header by default, so no action is needed on the static-site side.

**Priority: P2** -- No fix needed. Noted for completeness.

---

## 3. XSS Vectors

**Verdict: PASS**

| Check | Result |
|---|---|
| innerHTML usage | None |
| URL parameter reading (location.search, location.hash) | None |
| eval / Function constructor | None |
| document.write | None |
| User input handling | None (buttons only toggle lang) |
| localStorage injection risk | See 3.1 below |
| Dynamic DOM creation from untrusted data | None |

### Issue 3.1 -- localStorage read is safe but worth noting (PASS, no fix needed)

Both files read `localStorage.getItem('deenlog-lang')` (index.html line 838, privacy.html line 413) and compare it strictly against `'de'` or `'en'`. The value is never interpolated into HTML or used in any DOM-writing operation. The comparison is a hardcoded equality check, so even a tampered localStorage value would simply fall through to the browser-locale default. No vulnerability here.

---

## 4. External Dependencies

**Verdict: PASS**

| Check | Result |
|---|---|
| Third-party JS (CDNs, libraries) | None |
| External CSS (Google Fonts, etc.) | None |
| Analytics / tracking pixels | None |
| External images | None -- all images are local (`screens/`) or data-URI |
| Fonts from external origins | None -- system font stack only (`-apple-system`, etc.) |
| iframes | None |

Both files are fully self-contained. All CSS is inline, all JS is inline, all assets are local. This is the ideal state for a privacy-focused marketing site.

---

## 5. Privacy Compliance

**Verdict: PASS (with one P2 note)**

### 5.1 -- Privacy policy matches actual site behavior (PASS)

The privacy policy states:
- All data stored locally -- **Correct.** The website itself stores only `deenlog-lang` in localStorage (a UI preference, not personal data).
- No website-side analytics or data collection -- **Correct.** No outbound requests to any non-GitHub domain.
- No crash reporting / analytics -- **Correct.** No scripts of any kind load from external origins.

The policy is written for the iOS app, not the website, which is fine -- the website collects even less data than the app.

### 5.2 -- GDPR considerations for DE market (P2)

The site targets a German audience (bilingual DE/EN). Under GDPR and the German TTDSG:

- **Cookies:** The site sets no cookies. PASS.
- **localStorage:** The site writes one key (`deenlog-lang`). Under TTDSG section 25, storing information on a user's device requires consent unless it is "strictly necessary" for the service the user explicitly requested. A language preference toggle activated by user click is arguably strictly necessary for the feature the user requested. This is low-risk but could be made airtight by only writing to localStorage after the user explicitly clicks a language button (which is already the case -- the initial `setLang()` call on page load also writes, but this is setting a preference based on browser locale detection, which is standard practice).

- **Impressum (Imprint):** German law (TMG section 5 / DDG section 5) requires a legal notice ("Impressum") on commercial websites. The current site has no Impressum link. If the site is considered commercial (it promotes an app on the App Store), an Impressum is legally required for German-facing deployment.

**Recommended fix:** Add an Impressum page or a clearly visible Impressum section, containing at minimum:
- Full name (Serdar Saglam)
- Postal address
- Email contact
- A statement that this is a non-commercial / personal project (if applicable, to claim the TMG exemption)

**Priority: P2** -- Legal compliance item. Not a security vulnerability, but required by German law for commercial sites. Consult a legal resource to determine if the TMG/DDG exemption for purely personal sites applies.

---

## Summary

| # | Category | Verdict | Issues |
|---|---|---|---|
| 1 | Sensitive data exposure | PASS | 1.1 Email scraping (P1), 1.2 Placeholder URL (P2) |
| 2 | Security headers | FAIL | 2.1 Missing CSP (P1), 2.2 Missing Referrer-Policy (P1), 2.3 No XCTO meta (P2, N/A) |
| 3 | XSS vectors | PASS | None |
| 4 | External dependencies | PASS | None (fully self-contained) |
| 5 | Privacy compliance | PASS | 5.2 Missing Impressum for DE (P2) |

### Action items before deploy

**P1 (should fix):**
1. Add `Content-Security-Policy` meta tag to both HTML files (issue 2.1)
2. Add `Referrer-Policy` meta tag to both HTML files (issue 2.2)
3. Obfuscate email addresses in mailto: links (issue 1.1)

**P2 (nice to have):**
4. Replace placeholder App Store URL or hide CTA (issue 1.2)
5. Add Impressum for German legal compliance (issue 5.2)

No P0 (must-fix-immediately) issues were found. The site is clean, self-contained, and free of common web security pitfalls. The P1 items are low-effort hardening measures that take about 10 minutes total to implement.
