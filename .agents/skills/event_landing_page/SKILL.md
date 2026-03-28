---
name: event_landing_page
description: A responsive, single-page landing page templates for local events. Features a natural/earthy aesthetic, timeline layout, pricing grid, photo gallery, and LINE Official Account CTA integration.
---

# Event Landing Page Skill

This skill defines the structure and styling principles for creating highly engaging, single-page HTML/CSS landing pages for local events (e.g., cycling tours, workshops, gatherings).

## 1. Tech Stack
- **HTML5**: Semantic tags (`<header>`, `<main>`, `<section>`).
- **Vanilla CSS3**: CSS Variables for theming, Grid & Flexbox for layout. No external frameworks (Tailwind, Bootstrap) to keep it dependency-free.
- **Vanilla JS**: Minimal JavaScript strictly for UI micro-interactions (e.g., `IntersectionObserver` for fade-in animations, `navigator.clipboard` for copying templates).

## 2. Design System & CSS Variables
Define the core theme using native CSS variables on the `:root` pseudo-class. For natural, approachable events, use earthy and warm tones:

```css
:root {
  --bg-color: #f9f6f0;       /* Main soft background */
  --bg-earth: #f4eee1;       /* Alternate card background */
  --text-main: #3d352d;      /* Deep rich text (avoid pure black) */
  --text-light: #6a6053;     /* Subtitle/mute text */
  --accent-green: #6d8c6b;   /* Primary accent */
  --accent-orange: #d17a47;  /* Secondary/CTA accent */
  --accent-yellow: #e8c366;  /* Highlights */
  --white: #ffffff;
  --card-shadow: 0 10px 30px rgba(61, 53, 45, 0.06);
  --border-radius-lg: 24px;
  --border-radius-md: 16px;
  --transition: all 0.3s ease;
}
```

## 3. Core Structural Patterns

### A. Hero Section (Stacking Contexts)
A full-height hero section with a dynamic background image and an overlay.
**Critical Rule**: Prevent overlapping `z-index` bugs with upcoming negative-margin sections by explicitly defining stacking contexts.
```css
.hero { position: relative; z-index: 1; height: 80vh; ... }
.hero-bg { position: absolute; ... z-index: 1; }
.hero-overlay { position: absolute; ... z-index: 2; }
.hero-content { position: relative; z-index: 3; }
```

### B. Negative Margin Intro Block
To seamlessly bridge the hero section and the main content, use a negative `margin-top` on the first container, ensuring its `z-index` is higher than the `.hero`.
```css
.intro { position: relative; z-index: 10; margin-top: -80px; }
```

### C. Photo Gallery Grid
For displaying multiple images elegantly (e.g., 1 large + 2 small):
```css
.photo-gallery { display: grid; grid-template-columns: repeat(2, 1fr); gap: 15px; }
.photo-gallery img:first-child { grid-column: span 2; aspect-ratio: 16/9; }
.photo-gallery img:not(:first-child) { aspect-ratio: 4/3; }
```

### D. CSS-Only Timeline
Construct event schedules using a `<ul>` list with `::before` pseudo-elements for the connecting line and list marker dots.
```css
.timeline { position: relative; }
.timeline::before { /* vertical line */ content: ''; position: absolute; left: 11px; width: 2px; }
.timeline li { position: relative; padding-left: 35px; }
.timeline li::before { /* dots */ content: ''; position: absolute; left: 0; top: 6px; width: 20px; height: 20px; border-radius: 50%; }
```

## 4. LINE Official Account CTA Integration
Converting visitors requires a frictionless CTA. Use a direct LINE open link combined with a tap-to-copy message template.
- **Link Format**: `https://line.me/R/ti/p/%40<LINE_ID>` (Always URL-encode the `@` as `%40`).
- **Copy Template**: Use inline JS to allow users to copy a template easily.
```html
<div class="cta-buttons">
    <a href="https://line.me/R/ti/p/%40XXXXXXXX" target="_blank" class="btn-primary">LINEを開いて申し込む</a>
</div>
<div class="copy-template" onclick="navigator.clipboard.writeText('Template Text'); alert('Copied!');">
   ...Template Text...
</div>
```

## 5. Micro-Animations
Use `IntersectionObserver` to trigger a generic `.fade-up` class when scrolling.
```css
.fade-up { opacity: 0; transform: translateY(40px); transition: opacity 0.8s, transform 0.8s; }
.fade-up.visible { opacity: 1; transform: translateY(0); }
```

## Usage
When tasked to create an event landing page, inject this structure, adapt the CSS root variables to fit the event's vibe (e.g., Beach event = blues/yellows), and construct the components mapping precisely to this markdown reference.
