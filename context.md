# Lab Access Ghana — Project Context

> Single-page marketing site for **Lab Access**, a licensed diagnostic centre in
> Teshie, Accra. This doc is the handoff brief: read it first, then `index.html`.
> Last updated: 2026-06-02.

---

## 1. What this is

A **static website** — plain HTML + CSS + vanilla JS. No framework, no build step,
no package.json. You edit the files and they ship as-is.

- **Live URL:** https://labaccessghana.com
- **Repo:** https://github.com/blakrisemarketing-spec/lab-access-ghana
- **Deploy branch:** `main` (Hostinger auto-deploys from it — see §6)
- The current working branch in this worktree is `claude/elated-spence-f77cb9`;
  changes are pushed to `main` via `git push origin HEAD:main`.

## 2. File structure

```
index.html                 # the entire site (one page, anchor-nav sections)
css/
  tokens.css               # design tokens (colours, type scale, spacing, motion)
  styles.20260602c.css     # all component styles  ← NOTE the dated filename (see §6)
js/
  main.js                  # contact form → WhatsApp, smooth scroll, mobile menu toggle
images/                    # logo, hero, about, founder, package photos
robots.txt, sitemap.xml    # reference https://labaccessghana.com
.claude/launch.json        # local preview config (python http.server on :4178) — gitignored
```

> **The stylesheet filename is intentionally versioned** (`styles.20260602c.css`).
> Every time you change the CSS you must rename it to a new, never-used name and
> update the `<link>` in `index.html`. This is a cache-busting workaround — see §6.
> The page links `css/tokens.css` then the dated `styles.*.css` (tokens is also
> `@import`-ed at the top of the styles file, so tokens load regardless).

## 3. Sections of the page (top → bottom)

1. **Navbar** — logo (left), anchor links (Services/Packages/About/Contact), and a
   **call button** (`.navbar__call`, orange pill + phone icon → primary phone number).
2. **Hero** — orange gradient. H1 "Reliable. Convenient. Confidential Reports.",
   sub-line, "Book via WhatsApp" + "Call to book" buttons.
3. **Vision / Mission / Core Values** (`.vmv`) — 3 cards (replaced the old stats strip).
4. **About Us** (`#about`, `.split`) — blood-sample photo + company copy + "Licensed by
   HeFRA" badge.
5. **A note from our founder** (`#founder`, `.founder`) — Perpetual Karikari's photo +
   message. Has a soft warm tint background (`#FCF2E8`) to stand apart.
6. **What we test** (`#services`) — `.spec-sheet` table of tests + turnaround times.
7. **Health packages** (`#packages`) — `.product-grid` of 8 package cards with prices.
   A `.section__note` states packages exclude consultation/hardcopy; reports go via the
   BetterHealth app (https://betterhealth.africa) or office pickup.
8. **What clients say** — 6 real testimonials.
9. **Get in touch** (`#contact`) — WhatsApp-powered contact form + phone/WhatsApp/hours/
   location blocks + Google Map embed.
10. **FAQ** (`#faq`) — `<details>` accordions.
11. **Footer** — logo, links, **social icons** (Facebook/Instagram/Threads), legal.
12. **Mobile sticky CTA** (`.mobile-cta`) — Call + WhatsApp buttons (mobile only).

## 4. Design system (BRAND ORANGE theme)

The site was originally medical-blue; the owner (Perpetual) approved **orange** (the
logo colour) as final on 2026-06-02. Blue is fully removed.

Colour tokens (`css/tokens.css`):
- `--color-accent: #C2410C` — **deep orange** for links / small text on white.
  Chosen because it passes WCAG AA (contrast 5.2 on white). Used everywhere via `var()`.
- `--brand-bright: #F7941E` — the **bright logo orange**. Used on buttons (with DARK
  text `#1a1a2e`) and decorative accents (card top-borders, list bullet dots, the
  featured badge, the founder quote mark). Bright orange + white text FAILS contrast
  (~2.3), so bright orange always pairs with dark text.
- `--color-accent-hover: #9A3412`, `--color-focus: #F2820C`.
- Hero gradient (in styles): `linear-gradient(135deg, #F4870E 0%, #A8390A 100%)` with a
  text-shadow on `.hero__display/.hero__lede` for legibility of white text.

**Rule of thumb when adding UI:** deep orange (`--color-accent`) for text/links;
bright orange (`--brand-bright`) only with dark text or for decoration.

Fonts: Inter (display + body), JetBrains Mono (small labels/credentials). Type scale is
a 1.25 major-third in tokens. Responsive breakpoints at 960px and 640px (375px tweaks).

## 5. Key data / content facts

- **Primary call number:** `024 7575 668` → `tel:+233247575668`, displayed
  `+233 24 7575 668`. It's in the navbar button, hero "Call to book", footer, mobile
  CTA, and first in the contact list. (Changed from the old 030 number on 2026-06-02;
  the 030 `+233 302 729 434` and 050 `+233 504 972 604` remain as secondary contact-list
  entries.)
- **WhatsApp number:** `233504972604` (used by the contact form in `js/main.js` and all
  `wa.me` links). Note this is the 050 number, not the primary call number.
- **Map:** embed query `LAB ACCESS MEDICAL LABORATORY, Teshie, Accra` (the real Google
  listing; coords ≈ 5.6063163, -0.122646).
- **Hours:** Mon–Sat 8am–5pm; Public holidays 8am–2pm.
- **Location:** Teshie, Lekma-Manet Road, Paris Villa (GZ-130-6688).
- **Established:** 2019 (footer/about say 2019 — do not reintroduce "2009"/"15+ years").
- **Social:** FB facebook.com/labcourier · IG instagram.com/lab_access · Threads
  threads.com/@lab_access.
- **Licensing:** "Licensed by HeFRA" (about badge + footer legal).

## 6. Deployment & the CACHING GOTCHA (read before you ship)

- Push to `main` (`git push origin HEAD:main`). There is **no GitHub Action**; Hostinger's
  own Git integration auto-deploys `main` to the web root behind its `hcdn` CDN.
- **Deploy lag is real and large.** It can take several minutes — sometimes 10+ — for a
  push to appear, and the CDN can briefly serve an *older* cached `index.html` from some
  edges before catching up. Don't panic; poll and wait.
- **Static assets (css/js/images) are sent with `cache-control: max-age=604800` (7 days)
  and the CDN ignores query strings.** Consequences:
  - A `?v=...` query-string cache-bust **does NOT work** here.
  - If you change CSS but keep the same filename, the old CSS can be served for up to a
    week. **So: rename the stylesheet to a brand-new filename on every CSS change** and
    update the `<link>` in `index.html`. That's why it's `styles.20260602c.css` (the
    `a`/`b`/`c` suffixes are successive same-day renames). HTML (`index.html`) is NOT
    long-cached, so its filename stays constant.
- **Verifying the live site:** request **bare URLs** (no `?cb=` query). Appending a random
  query string can return a misleading 404 from the CDN even when the bare path is 200.
  Example check:
  ```
  curl -s -o /dev/null -w '%{http_code}' https://labaccessghana.com/css/styles.20260602c.css
  curl -s https://labaccessghana.com/ | grep -c 'A note from our founder'
  ```
- If a deploy genuinely stalls, the fallback is to **purge cache / manually Deploy in
  Hostinger hPanel → Websites → Advanced → Git** (requires the owner's Hostinger access;
  not doable from the CLI here).

### ⚠️ Current state at handoff (2026-06-02)
All work below is committed and pushed to `main` (HEAD = `a1e8cbe`). At the moment of
writing, the live site had **not yet** propagated the last three commits (it was still
serving `styles.20260529.css` with no founder section, and the newer assets 404'd at
origin) — consistent with the deploy lag above. **Action for next agent:** poll the live
site until `styles.20260602c.css` returns 200 and the page contains "A note from our
founder" and `navbar__call`. If it hasn't caught up after ~15–20 min, ask the owner to
trigger a manual deploy / cache purge in Hostinger hPanel.

## 7. Local preview

`.claude/launch.json` runs `python3 -m http.server 4178`. Or just open `index.html`.
When screenshotting via the preview tool, note its eval/layout context can report a
0-width viewport (measurements read 0) — trust screenshots over `getBoundingClientRect`,
and the screenshot captures from the top of the page.

## 8. Change history (most recent first)

- `a1e8cbe` Header phone number → orange call button (`.navbar__call`).
- `20a382b` Founder note warm tint (`#FCF2E8`) + tighter para gap (0.5rem); 024 made the
  primary call number sitewide.
- `c8451ac` Orange became the real theme (blue removed); added founder's note section;
  removed the temporary `orange-preview.html` / `theme-orange.css`.
- `aca1e87` (superseded) Added a standalone `orange-preview.html` so the owner could
  compare orange vs blue before approving.
- `9dfb3ad` Map pointed at the real Google listing; added footer social links.
- `3d64733` About image swapped to the blood-sample photo (`about-blood-sample.jpg`);
  removed unused `about-lab-team.*`.
- `8fab9e5` First stylesheet rename to defeat the CDN cache.
- `9ce5cdd` Lab Access team's first round of edits (hero copy, Vision/Mission/Values,
  service turnarounds, packages note, real testimonials, FAQ edits, hours/location,
  HeFRA, bigger logo, footer date 2019).

## 9. Open items / nice-to-haves

- **WebP/optimisation:** `about-blood-sample.jpg` and `founder-perpetual.jpg` are plain
  JPEGs (no WebP variant — `cwebp` wasn't available in the build env). Some legacy PNGs
  in `images/` are large (1–2 MB, e.g. `hero-lab-access.png`, `about-lab-closeup.png`)
  and may be unused — safe to audit/remove.
- The contact form's `<select>` options don't match the current package names — could be
  aligned with the 8 real packages.
- If the owner ever wants white text on bright-orange buttons, that's an accessibility
  compromise (flag it).
- Consider folding the dated stylesheet back to a stable name + a real cache-busting
  story if the Hostinger CDN config can be changed (would remove the rename ritual).
