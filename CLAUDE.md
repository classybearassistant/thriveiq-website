# ThriveIQ Website — CLAUDE.md
*Read this in full before touching index.html. This is the locked design system — do not deviate without founder approval.*

---

## REPO MECHANICS

- Single file: `index.html` — large, use targeted string/regex replacement, never rewrite wholesale
- Push: `git add . && git commit -m "..." && git push` — Cloudflare Pages auto-deploys in 60–90 seconds
- This repo is SEPARATE from the app repo (`~/Desktop/Macro-Wellness-App`). Do not cross-apply app design rules (dark background, branded label rules, app score labels) here unless explicitly told to match the app for a specific page.

## PROCESS RULES (non-negotiable — mirrors the app repo's Regression Pattern rule)

1. **Diagnostic first, always.** Before any fix: grep/read the actual current markup and CSS. Never assume prior session notes describe the live state — they may be stale or wrong (this has happened repeatedly: a prior "buttons squared" claim turned out to be false; a "nav logo fixed" claim actually only fixed the footer logo, not the header).
2. **One consolidated fix per pass.** Diagnose → report findings → single fix → verify → push. Never stack unverified changes.
3. **Verify by screenshot before moving on.** "Committed and pushed" does not mean "correct on the live site." Founder confirms visually.
4. **Never touch more than the scoped fix.** If you notice something else wrong while in there, flag it — don't fix it silently in the same pass.
5. **Check for multiple instances of the same element.** This site has near-duplicate markup in more than one place (e.g., header nav logo vs. footer logo are two completely different code blocks, not one shared component). Grep broadly before declaring something fixed.

## DESIGN SYSTEM (locked)

**Background:** light cream/mint gradient (~#F1F6F1 to white) — NOT dark like the app.

**Colors:**
- `--teal: #1D9E75` (primary brand teal — do not let off-brand variants like #2D8C8C or #4ECDC4 creep back in as the PRIMARY brand color; #4ECDC4 exists only as `--teal-light`, a secondary/hover shade)
- `--teal-light: #5DCAA5`
- `--sage: #7A9E7E`, `--sage-light: #B8D4BA`, `--sage-pale: #EBF3EC`
- `--gold: #C9A84C`
- `--charcoal: #1C1C1E`

**Typography:**
- Headlines: Playfair Display (serif), bold, black (#1A1A1A) — italic teal for emphasized phrases
- Body: DM Sans
- Labels/tags/mono accents: DM Mono
- Never Georgia/System UI/Courier New on the website — those are app-only fonts

**Buttons — ALL squared, borderRadius 8px. No exceptions, including decorative pills.**
As of Aug 16, 2026: this covers every clickable CTA AND every decorative pill/badge/tag on the site — hero-eyebrow, download-badge, feature-tag, nav-cta, btn-primary, btn-secondary, newsletter-btn, app-store-btn, waitlist "Notify me" button. If you find a `border-radius: 100px` or any pill-shaped radius anywhere on this site, it's a bug — square it to 8px.

**Logo — real asset only, never emoji, never hand-drawn SVG approximations.**
- The real icon-only mark lives at `images/logo-icon.png` (leaf + EKG pulse, transparent background, teal #1D9E75)
- Never use the 🌿 emoji as a stand-in for the logo anywhere on the site
- Never hand-draw a new inline `<svg>` leaf shape as a "close enough" substitute for the real asset — if a new logo placement is needed, use the actual PNG/SVG asset file
- **Known duplicate-markup risk:** header nav logo and footer logo are separate code blocks. If asked to update "the logo," check BOTH locations, not just one.

**Buttons container example (reference only, confirm live CSS before editing):**
```css
border-radius: 8px; /* not 100px */
```

## OPEN ITEMS (check before assuming resolved)

- Header nav logo sizing/spacing — leaf icon reported too small, gap between icon/divider/wordmark reported too large as of Aug 16, 2026. NOT YET FIXED. Get current markup via grep before touching.
- Doctor Visit Prep blog card — screenshot exists (`blog-doctor-visit-prep.jpg`) but not wired in; no natural existing card slot. Do not add without founder decision on which card to use or whether to add an 11th card.
- Sleep blog post — drafted and legal-audited, NOT yet approved, NOT live, NOT in blog-feed.json. Do not publish without explicit founder go-ahead.
- 7 of 10 homepage blog cards still use original hand-drawn SVG icons (only Seed Oils, CGM, Cholesterol have been swapped to real screenshots so far). Fine as-is unless founder requests more swaps.

## PRE-EXISTING CONTENT BUGS (documented, not yet fixed — do not fix without founder sign-off since scope/intent unclear)

- "Normal vs Optimal" card links to `normal-vs-optimal.html` but labeled category "Autoimmune" — mismatch, unclear if intentional
- Hydration card ("You're Probably Dehydrated...") href points to `thyroid.html` — wrong link target
- Two cards both link to `fasting-insulin.html` — probably intentional (one article likely covers both) but unconfirmed

---

*Update this file whenever a design decision changes. This file is the source of truth for Code on this repo — keep it current or Code will drift.*
