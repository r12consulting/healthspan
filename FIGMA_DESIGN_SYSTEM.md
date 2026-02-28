# Figma Design System Rules — HealthSpan Concierge Medicine

> This file describes how to translate Figma designs into this codebase.
> Stack: plain HTML · Tailwind CSS (CDN) · vanilla JS · single `index.html`

---

## 1. Design Tokens

### Colors

All tokens are CSS custom properties defined in `:root` inside `index.html`'s `<style>` block **and** registered in the `tailwind.config` script. Always use the custom property or the Tailwind alias — **never** hardcode hex values.

| Token | Hex | Tailwind alias | Usage |
|---|---|---|---|
| `--forest` | `#3E4E44` | `forest` | Body text, primary backgrounds, buttons |
| `--forest-deep` | `#2C3830` | `forest-deep` | Dark headers, deep backgrounds |
| `--clay` | `#C7BBA4` | `clay` | Borders, muted accents, decorative markers |
| `--azure` | `#60B2D5` | `azure` | Focus rings, accent highlights |
| `--azure-dk` | `#1A6F8E` | *(CSS var only)* | Labels, links, arrow icons |
| `--azure-lt` | `#8FCCE3` | *(CSS var only)* | Light-theme label variant |
| `--cream` | `#F6F4EF` | `cream` | Primary page background |
| `--cream-mid` | `#EDE9E1` | `cream-mid` | Alternate section background |
| `--cream-card` | `#FDFCF9` | *(CSS var only)* | Card backgrounds, form inputs |

**Section backgrounds** use utility classes — not Tailwind color utilities:
```html
<section class="bg-cream">   <!-- #F6F4EF -->
<section class="bg-mid">     <!-- #EDE9E1 -->
<section class="bg-forest">  <!-- #3E4E44 -->
<section class="bg-deep">    <!-- #2C3830 -->
```

### Typography

```css
--font-d: 'Cormorant Garamond', Georgia, serif;   /* display / headings */
--font-s: 'Inter', system-ui, sans-serif;          /* body / UI */
--ease:   cubic-bezier(.4,0,.2,1);                 /* all transitions */
```

Google Fonts loaded: `Cormorant Garamond` (300–600, italic variants) + `Inter` (300–600).

---

## 2. Typography Scale

### Heading classes

```html
<!-- Section label (eyebrow) -->
<span class="label">Precision Medicine · Healing Arts</span>
<span class="label label--lt">Light variant (on dark bg)</span>

<!-- Section heading -->
<h2 class="heading">Growing outward, not just upward.</h2>
<h2 class="heading heading--lg">Larger variant</h2>
<h2 class="heading heading--lt">Light (on dark bg)</h2>

<!-- Page H1 only -->
<h1 class="heading heading--h1">Hero headline</h1>

<!-- Body subtext under section heading -->
<p class="subtext">Introductory paragraph…</p>
<p class="subtext subtext--lt">Light variant (on dark bg)</p>
```

| Class | Font | Size (clamp/fixed) | Weight | Color |
|---|---|---|---|---|
| `.label` | Inter | 0.6875rem | 500 | `--azure-dk` |
| `.heading` | Cormorant Garamond | clamp(2rem, 3.5vw, 3rem) | 400 | `--forest-deep` |
| `.heading--lg` | Cormorant Garamond | clamp(2.25rem, 3.5vw, 3.25rem) | 400 | `--forest-deep` |
| `.heading--h1` | Cormorant Garamond | clamp(2.5rem, 4.8vw, 4.25rem) | 400 | `--forest-deep` |
| `.subtext` | Inter | 1.0625rem | 400 | `rgba(62,78,68,.78)` |
| `.card-h` | Cormorant Garamond | 1.5rem | 500 | `--forest` |

### Body text (inline styles)
- Standard body: `font-size:.9375rem; line-height:1.7; color:var(--forest)`
- Paragraph body: `font-size:1rem; line-height:1.8; color:rgba(62,78,68,.78)`
- Small/meta: `font-size:0.6875rem; font-weight:500; letter-spacing:0.14em; text-transform:uppercase; color:var(--clay)`

---

## 3. Layout System

### Wrappers (horizontal centering + max-width)

```html
<div class="wrap">        <!-- max-width: 80rem; padding-inline: 4rem -->
<div class="wrap--wide">  <!-- max-width: 88rem; padding-inline: 4rem -->
<div class="wrap--narrow"><!-- max-width: 60rem; padding-inline: 4rem -->
```

### Section containers

```html
<section class="section">           <!-- padding-block: 6rem -->
<section class="section section--sm">  <!-- padding-block: 5.5rem -->
<section class="section section--lg">  <!-- padding-block: 7rem -->
<section class="section section--hero"><!-- padding: 5rem top, 12rem bottom -->
```

Always pair with a background class: `bg-cream`, `bg-mid`, `bg-forest`, `bg-deep`.

### Section header pattern

```html
<div class="sh">           <!-- centered -->
<div class="sh sh--left">  <!-- left-aligned -->
  <span class="label">Eyebrow text</span>
  <h2 class="heading">Section heading</h2>
  <p class="subtext">Optional intro paragraph.</p>
</div>
```

### Grids

| Class | Columns | Gap | Use case |
|---|---|---|---|
| `.g2` | `1fr 1fr` | 1.75rem | Generic 2-col |
| `.g3` | `repeat(3,1fr)` | 0.875rem | Benefit/feature grid |
| `.g3-lg` | `repeat(3,1fr)` | 3rem | Large 3-col |
| `.g4` | `repeat(4,1fr)` | 2.5rem | 4-col (collapses to 2 at tablet) |
| `.g-hero` | `1fr 1fr` | 4rem | Hero (text + image) |
| `.g-phil` | `1fr 1.6fr` | 5rem | Philosophy (logo + text) |
| `.g-cta` | `1fr 1fr` | 6rem | CTA split layout |
| `.g-foot` | `1.6fr 1fr 1fr` | 4rem | Footer 3-col |
| `.g2-inner` | `1fr 1fr` | 0.75rem / 1.5rem | Inner lists within cards |

---

## 4. Components

### Cards

```html
<!-- Elevated card (white) -->
<div class="card">
  <h3 class="card-h">Card heading</h3>
  <!-- content -->
</div>

<!-- Muted card (transparent tint) -->
<div class="card--muted">
  <h3 class="card-h">Card heading</h3>
</div>
```

### Benefit items (hoverable)

```html
<div class="benefit">
  <!-- icon + text content -->
</div>
```
Has `translateY(-1px)` hover lift + azure border glow.

### Pillars (numbered list on dark bg)

```html
<div class="pillar">
  <span class="pillar-n">01</span>
  <h3 class="pillar-h">Pillar title</h3>
  <p>…</p>
</div>
```

### Buttons

```html
<!-- Primary (forest green fill) -->
<a href="#" class="btn btn-primary">Request a Consultation</a>

<!-- Ghost (transparent + border) -->
<a href="#" class="btn btn-ghost">Learn More</a>

<!-- Full-width modifier -->
<a href="#" class="btn btn-primary btn--full">Full width</a>
```

Button rules:
- Font: Inter, 0.75rem, 500 weight, 0.1em letter-spacing, uppercase
- Border-radius: 2px
- Padding: 0.8125rem 1.875rem
- Transitions on `background-color`, `border-color`, `color`, `transform`, `box-shadow` only — **never** `transition-all`
- All buttons need `hover`, `focus-visible` (2px azure outline), and `active` states

### Navigation

Sticky nav with `backdrop-filter: blur(12px)`.

```html
<nav class="nav">
  <div class="nav__inner">
    <a class="nav__logo">…</a>
    <ul class="nav__links">
      <li><a href="#section" class="nav__link" data-nav="section">Label</a></li>
    </ul>
    <!-- desktop CTA + hamburger toggle -->
    <div>
      <a class="btn btn-primary nav__cta-desk">…</a>
      <button class="nav__toggle" aria-expanded="false">
        <span class="nav__bar"></span>×3
      </button>
    </div>
  </div>
  <!-- mobile drawer -->
  <div class="nav__drawer" id="nav-drawer">…</div>
</nav>
```

Active nav state: `.nav__link.active` — set by IntersectionObserver on `section[id]` elements.

### Form

```html
<form id="consult-form">
  <div class="form-row">          <!-- 2-col row (→ 1-col on mobile) -->
    <div class="form-group">
      <label class="form-label">Name</label>
      <input class="form-input" type="text">
    </div>
    <div class="form-group">…</div>
  </div>
  <div class="form-group">        <!-- full-width field -->
    <label class="form-label">…</label>
    <textarea class="form-input">…</textarea>
  </div>
</form>
<div id="form-success" class="form-success">…</div>  <!-- shown on submit -->
```

Error state: add `.error` class to `.form-input`.
Success state: add `.visible` class to `.form-success`.

### Footer links

```html
<a href="tel:+18085355555" class="flink">(808) 535-5555</a>
<a href="#" class="flink flink--sm">Small/legal link</a>
```

**Never** use inline `onclick` handlers for links — use `href` or the `.flink` class.

---

## 5. Decorative Patterns

### Radial gradient blobs

```html
<div aria-hidden="true" class="blob" style="
  top:-8%; right:-4%; width:55%; height:65%;
  background: radial-gradient(ellipse at 65% 35%, rgba(96,178,213,.08) 0%, transparent 68%);
"></div>
```

Place inside `.section`, use `position:relative;z-index:1` on the content wrapper above it.

### SVG wave divider

Used at the bottom of the hero. Layered paths with azure at low opacity (0.05–0.22).

### Grain texture overlay

Applied globally via `body::after` — a fixed SVG `feTurbulence` filter at `opacity:0.025`. Don't add per-section grain.

### Image treatment

```html
<div style="border-radius:4px; overflow:hidden;
  box-shadow: 0 4px 24px rgba(62,78,68,.12), 0 1px 6px rgba(62,78,68,.08);
  aspect-ratio:4/5; position:relative;">
  <img style="width:100%; height:100%; object-fit:cover;">
  <!-- Dark gradient overlay (bottom) -->
  <div aria-hidden="true" style="position:absolute; inset:0;
    background: linear-gradient(to top, rgba(44,56,48,.25) 0%, transparent 50%);"></div>
</div>
```

---

## 6. Shadows

Always use layered, color-tinted shadows. **Never** use flat `shadow-md`.

```css
/* Card */
box-shadow: 0 0 0 1px rgba(199,187,164,.25),
            0 1px 3px rgba(62,78,68,.06),
            0 4px 14px rgba(62,78,68,.05);

/* Button (primary) */
box-shadow: 0 1px 3px rgba(44,56,48,.25), 0 4px 12px rgba(44,56,48,.12);

/* Button (primary hover) */
box-shadow: 0 2px 6px rgba(44,56,48,.3), 0 8px 20px rgba(44,56,48,.15);

/* Benefit hover */
box-shadow: 0 2px 8px rgba(62,78,68,.1), 0 0 0 1px rgba(96,178,213,.2);
```

---

## 7. Responsive Breakpoints

| Breakpoint | Width | Key changes |
|---|---|---|
| Tablet | `≤1024px` | padding-inline → 2.5rem; `.g4` → 2-col; `.g-phil` → 1-col |
| Mobile | `≤768px` | padding-inline → 1.25rem; all grids → 1-col; hamburger nav shown |
| Small mobile | `≤480px` | H1 → 2.25rem; `.g3` → 1-col; tighter label tracking |
| Mid tablet | `640–768px` | `.g3` → 2-col exception |

---

## 8. Accessibility Conventions

- Skip link: `.skip-link` linking to `#main`
- All decorative elements: `aria-hidden="true"`
- Hamburger button: `aria-expanded`, `aria-controls`, `aria-label`
- Mobile nav: `role="navigation"`, `aria-label="Mobile navigation"`
- Focus styles: `2px solid var(--azure)` with `outline-offset: 3px` on all interactive elements
- `focus-visible` not `focus` (avoids click focus ring on mouse)

---

## 9. Icons

No icon library. Arrow `→` and cross `✕` are Unicode characters used inline:

```html
<!-- List item arrow (azure-dk) -->
<span aria-hidden="true" style="color:var(--azure-dk);font-size:1rem;margin-top:.15rem;flex-shrink:0;">→</span>

<!-- Negative/cross (clay) -->
<span aria-hidden="true" style="color:var(--clay);font-size:.875rem;margin-top:.2rem;flex-shrink:0;">✕</span>
```

---

## 10. Asset Management

- **Logo:** `brand_assets/logo.png` (monkeypod tree mark) — used at `height:46px` in nav, `max-width:300px` in philosophy section
- **Hero image:** `images/diamond-head-honolulu.jpg`
- **Placeholder images:** `https://placehold.co/WIDTHxHEIGHT` when real assets are absent
- No CDN. Assets are served from project root via `node serve.mjs` → `http://localhost:3000`

---

## 11. File Structure

```
healthspan/
├── index.html          ← entire site (HTML + <style> + <script>)
├── brand_assets/
│   └── logo.png
├── images/
│   └── diamond-head-honolulu.jpg
├── serve.mjs           ← dev server (node serve.mjs → :3000)
├── screenshot.mjs      ← puppeteer screenshotter
├── CLAUDE.md           ← Claude Code instructions
└── FIGMA_DESIGN_SYSTEM.md ← this file
```

All styles live in the `<style>` block inside `index.html`. No separate CSS files, no build step, no bundler.

---

## 12. Key Rules When Translating Figma Designs

1. **Colors:** Use CSS vars (`var(--forest)`) or Tailwind aliases (`text-forest`) — never raw hex.
2. **Fonts:** Headings always use `.heading` classes (Cormorant Garamond). Body uses Inter via `font-family:var(--font-s)`.
3. **Spacing:** Use established layout classes (`.wrap`, `.section`, `.g2` etc.) before writing custom spacing.
4. **Buttons:** Always use `.btn` base + `.btn-primary` or `.btn-ghost` modifier. Don't create new button styles.
5. **Grids:** Choose the closest existing grid class; only write custom `grid-template-columns` if no match exists.
6. **Shadows:** Layered, color-tinted only. Match the exact shadow pattern for the component type.
7. **Transitions:** Only animate `transform` and `opacity` (or individual properties like `background-color`). Never `transition-all`.
8. **New sections:** Follow the pattern — `.section` + background class + `.wrap` or `.wrap--wide` + `.sh` header.
9. **Dark sections:** Swap to `.heading--lt`, `.subtext--lt`, `.label--lt`, `.pillar-h` for text on dark backgrounds.
10. **Accessibility:** `aria-hidden="true"` on all decorative blobs, waves, and icon spans.
