# AXIOM Films — Portfolio Website
### Cinematic Photography & Videography Portfolio
*A fully responsive, single-file HTML portfolio with dark luxury theme*

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [File Structure](#2-file-structure)
3. [How to Use the File](#3-how-to-use-the-file)
4. [Section-by-Section Guide](#4-section-by-section-guide)
   - [Loader](#41-loader)
   - [Navbar](#42-navbar)
   - [Hero Slideshow](#43-hero-slideshow)
   - [Featured Work / Projects Grid](#44-featured-work--projects-grid)
   - [About Section](#45-about-section)
   - [Gallery & Lightbox](#46-gallery--lightbox)
   - [Testimonials](#47-testimonials)
   - [Services](#48-services)
   - [Contact Form](#49-contact-form)
   - [Footer](#410-footer)
5. [Design System — Colors & Fonts](#5-design-system--colors--fonts)
6. [How to Customize — Quick Reference](#6-how-to-customize--quick-reference)
7. [JavaScript Features Explained](#7-javascript-features-explained)
8. [Responsive Breakpoints](#8-responsive-breakpoints)
9. [Performance Notes](#9-performance-notes)
10. [Common Customizations (Copy-Paste Ready)](#10-common-customizations-copy-paste-ready)
11. [FAQ & Troubleshooting](#11-faq--troubleshooting)

---

## 1. Project Overview

This is a **single HTML file** portfolio website — all CSS and JavaScript are embedded directly inside it. You don't need a server, build tools, npm, or any dependencies installed. Just open the file in a browser.

**What's included:**
- Animated page loader with percentage counter
- Full-screen cinematic hero slideshow with film bars
- Filterable projects grid (All / Films / Photography / Commercial)
- About section with animated stat counters
- Masonry photo gallery with fullscreen lightbox
- Infinite-scroll testimonials carousel
- Services section with hover animations
- Contact form with simulated send
- Custom cursor, grain texture, and scroll-reveal animations

**Dependencies loaded from the internet (Google Fonts only):**
- `Cormorant Garamond` — display/heading font
- `DM Sans` — body font

If you need it to work fully offline, see [Section 10](#10-common-customizations-copy-paste-ready) for how to embed fonts locally.

---

## 2. File Structure

Since everything is in one file, here's the logical structure inside `axiom-portfolio.html`:

```
axiom-portfolio.html
│
├── <head>
│    ├── Google Fonts link
│    └── <style> ... all CSS ... </style>
│
└── <body>
     ├── .cursor / .cursor-follower     ← Custom mouse cursor
     ├── .loader                        ← Loading screen
     ├── <nav class="navbar">           ← Sticky navigation
     ├── .mobile-menu                   ← Mobile hamburger menu
     │
     ├── <section class="hero">         ← Hero slideshow
     ├── <section class="work">         ← Featured projects
     ├── <section class="about">        ← About / bio
     ├── <section class="gallery-section"> ← Masonry gallery
     ├── <section class="testimonials"> ← Client reviews
     ├── <section class="services">     ← Services list
     ├── <section class="contact">      ← Contact form
     ├── <footer class="footer">        ← Footer
     │
     └── <script> ... all JavaScript ... </script>
```

---

## 3. How to Use the File

**To view locally:** Just double-click `axiom-portfolio.html` — it opens in any browser.

**To deploy online:**
- Upload the single HTML file to any web host (Netlify, Vercel, GitHub Pages, etc.)
- No server-side code needed — it's 100% static

**To edit:**
- Open the file in any code editor (VS Code, Sublime Text, Notepad++)
- Use **Ctrl+F** (Find) to locate the section you want to change
- The code has comment banners like `/* ─── HERO ─── */` and `<!-- HERO SECTION -->` to help you navigate

---

## 4. Section-by-Section Guide

### 4.1 Loader

**What it does:** Shows an animated "AXIOM" logo with a gold loading bar and percentage counter when the page first loads. Fades out automatically.

**Where to find it in HTML:**
```html
<div class="loader" id="loader">
  <div class="loader-inner">
    <div class="loader-logo">AXIOM</div>   ← Change this text
    ...
  </div>
</div>
```

**How to change the name:**
Find `<div class="loader-logo">AXIOM</div>` and replace `AXIOM` with your name or brand.

**How to change the speed:**
In the JavaScript section, find `initLoader()`. The `60` in `setInterval(..., 60)` controls tick speed in milliseconds — lower = faster loader.

**How to remove the loader entirely:**
Delete the entire `<div class="loader" ...>` block from HTML, and delete the `(function initLoader() { ... })();` block from the JavaScript.

---

### 4.2 Navbar

**What it does:** Fixed top navigation bar. Becomes frosted/blurred after scrolling 60px. Has a hamburger menu on mobile.

**Where to find it:**
```html
<nav class="navbar" id="navbar">
  <div class="nav-logo">AXIOM</div>       ← Your brand name
  <ul class="nav-links">
    <li><a href="#work">Work</a></li>     ← Navigation links
    <li><a href="#about">About</a></li>
    ...
    <li><a href="#contact" class="nav-cta">Contact</a></li>  ← Gold CTA button
  </ul>
</nav>
```

**How to change nav links:** Edit the `<a href="#...">` tags. The `#work`, `#about` etc. correspond to the `id=""` on each section — keep them matching.

**How to change the blur threshold:** In JavaScript, find `navbar.classList.toggle('scrolled', window.scrollY > 60)` and change `60` to any pixel value.

**How to change the logo font size:** In CSS, find `.nav-logo` and adjust `font-size`.

---

### 4.3 Hero Slideshow

**What it does:** Full-screen background image slideshow with slow zoom (Ken Burns effect), cinematic black bars at top and bottom, and auto-advances every 6 seconds.

**Where to find the slides:**
```html
<div class="hero-slides" id="heroSlides">
  <div class="slide active" style="background-image: url('YOUR_IMAGE_URL')"></div>
  <div class="slide" style="background-image: url('YOUR_IMAGE_URL')"></div>
  <div class="slide" style="background-image: url('YOUR_IMAGE_URL')"></div>
  <div class="slide" style="background-image: url('YOUR_IMAGE_URL')"></div>
</div>
```

**How to change images:** Replace the `url('...')` values with your own image URLs or local file paths (e.g., `url('images/hero1.jpg')`).

**How to add/remove slides:**
- Add: Copy any `<div class="slide" ...>` line and paste it inside `.hero-slides`
- Remove: Delete a `<div class="slide" ...>` line
- **Important:** Also add/remove a matching `<span class="indicator" ...>` in `.hero-indicators` to keep the dots in sync

**How to change the slide interval:** In JavaScript, find `setInterval(next, 6000)` — change `6000` (6 seconds) to any value in milliseconds.

**How to change the hero text:**
```html
<p class="hero-eyebrow">Visual Storyteller · Est. 2009</p>   ← Small top label
<h1 class="hero-name">
  <span>A</span><span>x</span>...                            ← Main name
  <em>Films</em>                                             ← Italic word
</h1>
<p class="hero-tagline">Cinematographer & Visual Storyteller</p>  ← Tagline
<a href="#work" class="hero-cta"><span>View Work</span>...</a>    ← CTA button text
```

**How to remove the cinematic black bars:** Delete the two `<div class="hero-bar ...">` lines and their CSS rules (`.hero-bar`, `.hero-bar--top`, `.hero-bar--bottom`).

---

### 4.4 Featured Work / Projects Grid

**What it does:** An asymmetric grid of project cards with category filter buttons. Hover over a card to see the overlay with project title. First card spans 2 columns and 2 rows.

**Where to find a project card:**
```html
<article class="project-card" data-category="film">
  <div class="project-img" style="background-image:url('IMAGE_URL')"></div>
  <div class="project-overlay">
    <span class="project-cat">Film</span>      ← Category label
    <h3>The Last Light</h3>                    ← Project title
    <p>Feature documentary, 2024</p>           ← Subtitle / year
    <div class="project-arrow">↗</div>
  </div>
</article>
```

**How to add a new project:** Copy the entire `<article>` block and paste it inside `<div class="projects-grid">`. Change the image URL, category, title, and description.

**How to change filter categories:**
1. Change `data-category="film"` on the card to your category slug (e.g., `data-category="wedding"`)
2. Add a matching filter button: `<button class="filter-btn" data-filter="wedding">Wedding</button>`

**How to remove the large first card:** The CSS rule `.project-card:nth-child(1) { grid-column: span 2; grid-row: span 2; }` makes the first card big. Remove this rule to make all cards equal size.

---

### 4.5 About Section

**Where to find it:**
```html
<section class="about" id="about">
```

**How to change the profile photo:**
Find `<img src="https://images.unsplash.com/..." alt="Cinematographer portrait" />` and replace the `src` with your own image path.

**How to change the bio text:**
Find the `<p class="about-body">` paragraphs and replace the text. You can use `<em>word</em>` inside for italic gold-highlighted words.

**How to change the stats:**
```html
<span class="stat-num">15+</span>   ← The number (animated by JS)
<span class="stat-label">Years</span>  ← The label below
```
The numbers animate from 0 to their value when scrolled into view. The suffix (like `+`) is preserved automatically — anything non-numeric after the number is kept.

---

### 4.6 Gallery & Lightbox

**What it does:** A masonry (Pinterest-style) photo grid. Clicking any image opens a fullscreen lightbox. Navigate with arrow buttons or ← → keyboard keys. Press Escape to close.

**How to change gallery images — find this in JavaScript:**
```javascript
const galleryImages = [
  { src: 'https://your-image-url.jpg', caption: 'Your Caption Here' },
  { src: 'https://your-image-url.jpg', caption: 'Another Caption' },
  // Add or remove entries here
];
```

Each object needs two properties:
- `src` — the image URL (use `?w=800` for thumbnails, lightbox auto-loads `?w=1600` for full-res if using Unsplash)
- `caption` — text shown at the bottom of the lightbox

**How to change the number of columns:**
In CSS, find `.masonry-grid { columns: 4; }` and change `4` to `3` or `2` for fewer columns.

---

### 4.7 Testimonials

**What it does:** A horizontally scrolling infinite loop of review cards. Pauses when you hover over it.

**Where to find the cards:**
```html
<div class="t-card">
  <p>"Your testimonial text here..."</p>
  <footer><strong>Client Name</strong> · Title / Company</footer>
</div>
```

**Important:** The testimonials are duplicated (you'll see 5 cards, then the same 5 again). This is intentional — it creates the seamless infinite loop. When you add or remove cards, update **both sets** of cards (the original and the duplicate).

**How to change scroll speed:**
In CSS, find `animation: scrollTrack 40s linear infinite;` — lower the `40s` for faster scrolling.

---

### 4.8 Services

**Where to find a service item:**
```html
<div class="service-item">
  <div class="service-num">01</div>    ← Number
  <div class="service-body">
    <h3>Cinematic Films</h3>           ← Service title
    <p>Description text here...</p>   ← Short description
  </div>
  <div class="service-line"></div>     ← Gold hover line (leave this)
</div>
```

**How to add a service:** Copy the entire `<div class="service-item">` block and paste it inside `.services-grid`. Update the number, title, and description.

**Layout note:** Services sit in a 2-column grid. Odd items are on the left, even on the right. If you add a 7th service, it will be alone on the left of a new row.

---

### 4.9 Contact Form

**What it does:** A minimal form that collects Name, Email, Project Type (dropdown), and Message. On submit, it shows a success message. Currently simulates a send — no data goes anywhere.

**How to connect it to a real email service:**
Replace the `setTimeout(...)` block inside `initForm()` in JavaScript with a real API call. Recommended services: **Formspree**, **EmailJS**, or **Netlify Forms**.

Example with Formspree:
```javascript
// Replace the setTimeout block with:
const response = await fetch('https://formspree.io/f/YOUR_FORM_ID', {
  method: 'POST',
  body: new FormData(form),
  headers: { 'Accept': 'application/json' }
});
if (response.ok) {
  success.classList.add('visible');
  form.reset();
}
```

**How to change dropdown options:**
```html
<select id="project" name="project">
  <option value="" disabled selected>Project Type</option>
  <option>Cinematic Film</option>     ← Edit these
  <option>Photography</option>
  ...
</select>
```

**How to change contact links:**
```html
<a href="mailto:hello@axiomfilms.com" class="contact-link">
  hello@axiomfilms.com                ← Your email
</a>
<a href="https://instagram.com/yourhandle" class="contact-link">
  @axiomfilms                         ← Your Instagram handle
</a>
```

---

### 4.10 Footer

```html
<div class="footer-logo">AXIOM</div>                          ← Brand name
<p class="footer-copy">© 2025 Axiom Films. All rights reserved.</p>  ← Copyright
<div class="footer-socials">
  <a href="#">IG</a>    ← Replace # with your Instagram URL
  <a href="#">VIM</a>   ← Vimeo
  <a href="#">LI</a>    ← LinkedIn
</div>
```

---

## 5. Design System — Colors & Fonts

All colors are defined as CSS variables at the top of the `<style>` block. Change them once — they update everywhere.

```css
:root {
  /* Backgrounds */
  --black:      #080808;   /* Deepest background */
  --black-2:    #0d0d0d;   /* Alternate dark sections */
  --black-3:    #111111;   /* Services section */
  --grey-dark:  #1a1a1a;   /* Cards, form fields */
  --grey-mid:   #2a2a2a;   /* Borders */
  --grey-muted: #444444;   /* Muted text, inactive borders */
  --grey-light: #888888;   /* Secondary text */

  /* Text */
  --white:     #f5f0eb;            /* Main text (warm white, not pure) */
  --white-dim: rgba(245,240,235,0.6);  /* Dimmed text */

  /* Accent */
  --gold:       #b8955a;   /* Primary accent — buttons, labels, highlights */
  --gold-light: #d4ad77;   /* Lighter gold for italic text */

  /* Fonts */
  --font-display: 'Cormorant Garamond', serif;  /* All headings */
  --font-body:    'DM Sans', sans-serif;         /* All body text */
}
```

**To change the accent color from gold to another color** (e.g., a cool blue):
```css
--gold:       #4a8fc4;
--gold-light: #6aaae0;
```

**To change fonts:** Replace the Google Fonts `<link>` in `<head>` with different fonts, then update `--font-display` and `--font-body` in `:root`.

---

## 6. How to Customize — Quick Reference

| What to change | Where to find it | What to edit |
|---|---|---|
| Your name / brand | Search for `AXIOM` | Replace with your name |
| Hero tagline | `<p class="hero-tagline">` | Edit text |
| Hero images | `.slide` divs, `background-image: url(...)` | Change image URLs |
| Project photos | `.project-img` divs | Change `background-image` URLs |
| Project titles | `.project-overlay h3` | Edit text |
| About photo | `<img src="..." alt="Cinematographer portrait">` | Change src |
| Bio text | `<p class="about-body">` paragraphs | Edit text |
| Stats (15+, 200+) | `<span class="stat-num">` | Change numbers |
| Gallery images | `galleryImages` array in JS | Change src and caption |
| Testimonials | `.t-card` blocks | Edit text, name, title |
| Services | `.service-item` blocks | Edit number, h3, p |
| Contact email | `href="mailto:..."` | Your email address |
| Instagram handle | `href="#"` links in footer | Your social URLs |
| Footer copyright | `<p class="footer-copy">` | Edit year and name |
| Gold accent color | `--gold` in `:root` CSS vars | Any hex color |
| Section spacing | `--section-gap: 120px` in `:root` | Any pixel value |

---

## 7. JavaScript Features Explained

The JavaScript is split into 11 self-contained functions, each wrapped in `(function initX() { ... })();`. This means they're isolated — editing one won't break the others.

| Function | What it does |
|---|---|
| `initLoader()` | Animates the loading bar from 0–100%, then fades out the loader |
| `initCursor()` | Tracks mouse position for the custom dual cursor; uses `requestAnimationFrame` for smooth follower lag |
| `initNavbar()` | Adds `.scrolled` class after 60px scroll; toggles mobile menu open/close |
| `initSlideshow()` | Cycles hero slides every 6 seconds; handles indicator clicks |
| `initReveal()` | Uses `IntersectionObserver` to add `.visible` class when elements scroll into view, with staggered delays for sibling elements |
| `initFilter()` | Handles project grid filter buttons; hides/shows cards with a fade + scale transition |
| `initGallery()` | Builds the masonry grid from the `galleryImages` array; manages the lightbox open/close/navigate logic |
| `initForm()` | Intercepts form submit, simulates async send, shows success message |
| `initSmoothScroll()` | Makes all `<a href="#...">` links scroll smoothly with navbar offset |
| `initParallax()` | Moves hero content upward slightly as you scroll down (parallax effect) |
| `initCounters()` | Animates the stat numbers (15+, 200+, etc.) from 0 when they enter the viewport |

---

## 8. Responsive Breakpoints

The site has three breakpoints defined in CSS:

| Breakpoint | Max Width | Changes |
|---|---|---|
| Tablet | `1100px` | Projects grid: 3 columns; Gallery: 3 columns |
| Mobile Large | `900px` | Nav links hidden → hamburger; About stacks vertically; Projects: 2 columns; Services: 1 column |
| Mobile Small | `600px` | Reduced padding; Projects: 1 column; Gallery: 1 column; Section gap reduced to 60px |

To add a custom breakpoint, add to the bottom of the `<style>` block:
```css
@media (max-width: 1400px) {
  /* your rules */
}
```

---

## 9. Performance Notes

- **Images** use `loading="lazy"` where possible — they only load when near the viewport
- The **hero slides** load from Unsplash with `?w=1800` — replace with locally hosted images for faster load times
- The **lightbox** lazy-loads high-res versions (`?w=1600`) only when a gallery item is clicked
- The **grain animation** uses an SVG filter and CSS `animation` — it's GPU-accelerated and has near-zero CPU cost
- The **testimonials track** uses CSS `animation` (not JavaScript scroll) — also GPU-accelerated
- **Google Fonts** are the only external network request — preconnect tags are included to speed them up

---

## 10. Common Customizations (Copy-Paste Ready)

### Change the accent color to a deep emerald green
In `:root`, replace:
```css
--gold:       #2d7a5c;
--gold-light: #3fa876;
```

### Make the hero text left-aligned on mobile
In the `@media (max-width: 600px)` block, add:
```css
.hero-content { align-items: flex-start; }
```

### Add a 5th hero slide
In HTML, inside `.hero-slides`, add:
```html
<div class="slide" style="background-image: url('your-image.jpg')"></div>
```
And inside `.hero-indicators`, add:
```html
<span class="indicator" data-idx="4"></span>
```

### Disable the custom cursor (use default arrow)
Delete the `.cursor` and `.cursor-follower` divs from HTML, and delete the `initCursor()` function from JavaScript. Add to CSS:
```css
body { cursor: default; }
button { cursor: pointer; }
a { cursor: pointer; }
```

### Use local images instead of Unsplash URLs
1. Create an `images/` folder next to the HTML file
2. Put your images inside (e.g., `hero1.jpg`, `project1.jpg`)
3. Replace URLs like `https://images.unsplash.com/...` with `images/hero1.jpg`

### Embed fonts for offline use
Replace the Google Fonts `<link>` tags in `<head>` with:
```html
<style>
  @font-face {
    font-family: 'Cormorant Garamond';
    src: url('fonts/CormorantGaramond-Light.woff2') format('woff2');
    font-weight: 300;
  }
  /* repeat for each weight you use */
</style>
```
Download the font files from [Google Fonts](https://fonts.google.com).

### Connect the contact form to Formspree
1. Go to [formspree.io](https://formspree.io), create a free account, create a new form
2. Get your form ID (looks like `xabc1234`)
3. In JavaScript, inside `initForm()`, replace the `setTimeout` block with:
```javascript
form.addEventListener('submit', async (e) => {
  e.preventDefault();
  const res = await fetch('https://formspree.io/f/xabc1234', {
    method: 'POST',
    body: new FormData(form),
    headers: { 'Accept': 'application/json' }
  });
  if (res.ok) {
    form.reset();
    document.getElementById('formSuccess').classList.add('visible');
  }
});
```

---

## 11. FAQ & Troubleshooting

**Q: The fonts look wrong / plain.**
A: The Google Fonts link requires an internet connection. If you're offline, the browser falls back to the default serif and sans-serif fonts. Either go online or embed fonts locally (see Section 10).

**Q: The custom cursor doesn't show up.**
A: On touch devices (phones, tablets), the cursor is automatically hidden. This is intentional.

**Q: Images aren't loading.**
A: If using Unsplash URLs, you need an internet connection. For local images, make sure the file path is correct relative to the HTML file.

**Q: The lightbox arrows or close button don't work.**
A: Make sure you haven't accidentally deleted the `<button id="lightboxClose">`, `<button id="lightboxPrev">`, or `<button id="lightboxNext">` elements from the HTML.

**Q: I added a new project card but the filter doesn't work.**
A: Make sure your card has the `data-category` attribute set to one of the filter values (`film`, `photo`, `commercial`) or a custom one that matches a filter button's `data-filter` value.

**Q: The testimonials scroll too fast / too slow.**
A: Find `animation: scrollTrack 40s linear infinite;` in CSS and adjust the duration. Higher = slower.

**Q: The loader never goes away.**
A: This can happen if the JavaScript crashes before completing. Open your browser's Developer Tools (F12) → Console tab to see any error messages.

**Q: Can I add a video background to the hero instead of images?**
A: Yes. Replace the `.hero-slides` div with:
```html
<video class="hero-video" autoplay muted loop playsinline>
  <source src="your-reel.mp4" type="video/mp4">
</video>
```
And add this CSS:
```css
.hero-video {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: 0;
}
```

---

*Built with HTML, CSS, and vanilla JavaScript — no frameworks, no dependencies.*
*Designed for cinematographers, photographers, and visual storytellers.*
