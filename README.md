# 🍿 [Chronicle Popcorn](https://melissabangera.github.io/Chronicle-Popcorn/chroniclepopcornhome.html)

> *A Netflix-style dark-themed storytelling platform for true crime, horror, mystery, and psychological narratives.*

---

## Overview

Chronicle Popcorn is a single-file HTML landing page built with a cinematic dark aesthetic. It mimics the layout and feel of modern streaming platforms — horizontal scroll rows, hover card reveals, a full-screen hero, and smooth scroll animations — applied to a storytelling/reading platform.

---

## File Structure

```
chronicle-popcorn.html    ← Everything lives here (HTML + CSS + JS)
README.md                 ← This file
```

No frameworks. No build tools. No dependencies to install.
Just one file — open it in any browser and it works.

---

## Sections

| # | Section | Description |
|---|---------|-------------|
| 1 | **Navbar** | Fixed, transparent on load, turns solid black on scroll |
| 2 | **Hero** | Full-screen cinematic background with parallax + slow zoom |
| 3 | **Trending Now** | Horizontal scroll row with rank numbers (#1–#7) |
| 4 | **True Crime** | Genre row with hover card reveals |
| 5 | **Horror** | Genre row with hover card reveals |
| 6 | **Featured Banner** | Large cinematic mid-page spotlight section |
| 7 | **New This Week** | Responsive grid with NEW badges |
| 8 | **About** | Stats section with image collage |
| 9 | **Footer** | Four-column footer with links |

---

## Design System

### Color Palette

| Token | Hex | Usage |
|-------|-----|-------|
| `--bg` | `#0B0B0B` | Page background |
| `--card` | `#141414` | Card backgrounds |
| `--card-hover` | `#1c1c1c` | Card hover state |
| `--red` | `#E50914` | Accent — buttons, tags, highlights |
| `--red-dim` | `#b5070f` | Darker red for hover states |
| `--white` | `#FFFFFF` | Primary text |
| `--muted` | `#808080` | Secondary/meta text |
| `--dim` | `#3a3a3a` | Borders and dividers |

### Typography

| Role | Font | Usage |
|------|------|-------|
| Display | **Bebas Neue** | Section titles, hero headline, card titles |
| Serif | **Crimson Text** (italic) | Hero subheading, featured description, about body |
| Body | **Inter** | Navigation, metadata, buttons, footer |

All fonts are loaded from Google Fonts — requires an internet connection on first load.

---

## Features

### Animations & Interactions

- **Film grain overlay** — animated noise texture on `body::before`, loops every 0.8s, gives a cinematic film feel
- **Hero parallax** — background drifts upward as the user scrolls down
- **Hero slow zoom** — subtle `scale` keyframe animation on the hero background image
- **Navbar fade** — transparent → solid black with `backdrop-filter: blur` triggered at 60px scroll
- **Scroll reveal** — `.reveal` elements fade up into view using `IntersectionObserver`
- **Card hover** — story cards scale up, reveal title/meta overlay, and show a play button
- **Toast notifications** — bottom-right popup triggered by any card or button click

### JavaScript Modules

All JS is inline at the bottom of `<body>`, organized into clear sections:

```
DATA          → Story arrays (TRENDING, TRUE_CRIME, HORROR, NEW_RELEASES)
CARD BUILDERS → buildStoryCard(), buildReleaseCard() functions
POPULATE ROWS → Injects cards into each section on page load
NAVBAR SCROLL → Adds .scrolled class at 60px
HERO PARALLAX → translateY on scroll for depth effect
SCROLL REVEAL → IntersectionObserver watches .reveal elements
TOAST         → showToast(msg) utility used by all interactive elements
```

---

## How to Customize

### Swapping Story Content

All story data lives in arrays at the top of the `<script>` block:

```js
const TRENDING = [
  {
    title: "Your Story Title",
    tag: "True Crime",
    year: "2024",
    mins: "18 min read",
    img: "https://your-image-url.jpg"
  },
  // ...
];
```

Edit these arrays to change any row's content. The card HTML is generated automatically.

### Changing Hero Background

Find `.hero-bg` in the CSS and replace the `url(...)` value:

```css
.hero-bg {
  background:
    linear-gradient(to top, var(--bg) 0%, transparent 55%),
    linear-gradient(to right, rgba(0,0,0,0.85) 30%, transparent 75%),
    url('YOUR-IMAGE-URL-HERE') center/cover no-repeat;
}
```

### Changing Accent Color

Update `--red` in `:root` to any color:

```css
:root {
  --red: #E50914;   /* change this */
}
```

Every button, badge, tag, and highlight inherits from this single variable.

### Adding Real Links

All nav items, footer links, and story cards currently use `href="#"` or `onclick="showToast()"`. Replace these with real URLs or page routes when wiring up a backend.

---

## Responsive Behavior

| Breakpoint | Changes |
|------------|---------|
| `< 900px` | About section goes single-column, image collage hidden |
| `< 640px` | Nav links hidden, hero text scales down, story cards shrink |

---

## Fonts & External Resources

| Resource | URL | Required? |
|----------|-----|-----------|
| Google Fonts (Bebas Neue, Inter, Crimson Text) | fonts.googleapis.com | Yes — for typography |
| Unsplash images | images.unsplash.com | Yes — for all story card covers |

For a fully offline version, download the fonts and host images locally.

---

## Browser Support

Works in all modern browsers — Chrome, Firefox, Safari, Edge.
Internet Explorer is not supported (uses CSS custom properties and `IntersectionObserver`).

---

## Signature Design Element

The **animated film grain overlay** is the single most distinctive detail in this design. It runs as a fixed `body::before` pseudo-element using an inline SVG `feTurbulence` filter, animated with a jittery 8-frame loop. It gives the entire page the feel of watching something on old film stock — without any external library or image asset.

---

*Built for NovaNxt Lab — Chronicle Popcorn © 2025*
