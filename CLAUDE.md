# Cyberdelic Nexus — B2B One-Pager

Mobile-responsive marketing one-pager for Cyberdelic Nexus, pitching curated immersive experiences to events, venues, clinics, retreats and wellness centers.

## Entry point

`cyberdelic-nexus-onepager.html` — single self-contained page (HTML + inline CSS + minimal vanilla JS). Open it directly in a browser, or serve the folder with a local static server (e.g. `python3 -m http.server`) so the QR code CDN script loads cleanly.

## File layout

All assets sit flat in this folder alongside the HTML. The HTML references them by relative path (spaces are URL-encoded as `%20`). Reorganising into an `assets/images/` subfolder is fine, just update the `src` and `url()` references.

### Assets currently used by the page

- `Background_Option2.png` — full-page circuit-pattern background.
- `Cyberdelic Flower.png` — Cyberdelics framework diagram (hero centerpiece; left column of the two-column hero, no animation).
- `CN_Logo (Large).png` — Nexus emblem only (nav + footer).
- `CS Logo.png` — Cyberdelic Society icon (About).
- `CA Logo NL.png` — Cyberdelic Academy icon (About).
- `CL Logo NL.png` — Cyberdelic Labs icon (About, B2B division, highlighted).
- `CD Logo NL.png` — Cyberdelic Dojo icon (About).

### Assets present but not yet used

`CN Logo_V_B.png` (Nexus vertical lockup — was the hero logo, removed when the hero became two-column), `CS Logotype.png`, `CA Logotype.png`, `CL Logotype.png`, `CD Logotype.png`, `Cyberdelic Showcase_logytype.png`. Available if a section ever needs the division name lockups instead of the icon marks.

## Tech stack

- Vanilla HTML, CSS, JS. No build step.
- Google Fonts: Poppins (300–800).
- qrcodejs from cdnjs for the WEB and BOOK QR codes (renders client-side; clickable buttons are the always-working fallback).
- Animations use CSS keyframes and a small IntersectionObserver for scroll reveal.

## Conventions

- **Screen blend on dark-bg PNGs.** All logo and flower PNGs sit on a black background. They are displayed with `mix-blend-mode: screen` so the black drops out and they glow on the dark page. If a logo ever looks washed out, the fix is a transparent-background PNG, not removing the blend mode.
- **Glassmorphism.** Cards use `backdrop-filter: blur(22px) saturate(155%)` over the layered page background. The four background layers (`bg-img`, `bg-tint`, `blob` x3, `stars`) are what the glass actually blurs.
- **Background effects.** Slow Ken Burns drift on the circuit image, three color blobs drifting with `mix-blend-mode: screen` so purple/cyan/magenta light wash across the circuitry, soft vignette via `bg-tint`, twinkling starfield.
- **Brand gradient.** `linear-gradient(100deg,#4cdcef 0%,#b49bf8 50%,#e562a4 100%)`, exposed as the `--grad` CSS variable. Used for primary buttons, accents, and gradient text.
- **Section pattern.** Each section uses `eyebrow → s-title → underbar → s-lead` for a consistent header rhythm. Section padding is `clamp(62px, 8.5vw, 112px) 0`.
- **Reveal animations.** `.reveal` for individual elements, `.rgroup` for grids (children stagger via nth-child transition delays). Triggered by IntersectionObserver. `prefers-reduced-motion` disables all motion and forces revealed state.

## Section order (one-pager best practice)

> No nav bar — this page is designed to be embedded inside the main Cyberdelic Nexus website, so the sticky nav was removed. The hero is the first thing on the page.

1. Hero — two-column: Cyberdelic flower (left, no animation) + headline, CTAs (right)
2. Featured-in — trust bar
3. What We Offer — Cyberdelic Menu, 4 category cards
4. How It Works — 5 licensing packages + 1 CTA card
5. Why It Works — 4 value props
6. Proof of Concept — note + 3 stats
7. Testimonial
8. About — Nexus intro + 4 division logo rows
9. Network — festivals + research partners
10. Final CTA — Reach Out with 2 QR codes
11. Footer

## CTAs and links

- Book a call → `https://calendly.com/cyberdelicnexus/cyberdelic-nexus-meeting`
- Explore the experiences → `https://cyberdelic.nexus`
- Email → `connect@cyberdelic.nexus`
- WEB QR → `https://cyberdelic.nexus`
- BOOK QR → Calendly link above

Every "Book a call", "Enquire", and package CTA points at Calendly. Package "Enquire" links open in a new tab.

## Open items / TODO

- **Press logos for Featured-in.** Currently styled monochrome wordmarks. To upgrade: drop logo files for The Guardian, French Culture Radio, RTE Radio, Freethink, Frontiers, Science Open, National Institute of Health and British Computer Society into this folder and replace each `.lw-item` span in the HTML with an `<img>` of the matching logo.
- **Optional reorg.** Move PNGs into `assets/images/` and update relative paths if the flat layout becomes unwieldy.
- **Optional rename.** `cyberdelic-nexus-onepager.html` → `index.html` for web convention.
- **Optional hosting.** No server logic. Drop the folder on any static host (Netlify, Vercel, GitHub Pages, S3, Cloudflare Pages).

## Quick recipes

- **Swap a logo image.** Find the `<img>` in the HTML, change the `src` to the new filename (URL-encode spaces as `%20`). If the new logo has a transparent background, remove `mix-blend-mode: screen` from that element's CSS.
- **Add a new package card.** Duplicate one of the `<article class="card pkg">` blocks inside `#packages`. Update the SVG icon, `h3`, `p`, and keep the `.enquire` link pointing at Calendly.
- **Change brand gradient.** Update the `--grad` variable in `:root` (cyan→violet→magenta) — drives gradient text and accents. Primary CTA buttons use a separate, pink-free `--grad-cta` (cyan→violet) so the call-to-action avoids magenta; change that one to restyle buttons.
- **Tune background visibility.** Adjust the alpha stops in `.bg-tint` (lower = circuit pattern more visible, higher = darker for stronger text contrast).
