# Deepika D — Personal Portfolio Website

A fully accessible, semantic HTML5 personal portfolio website built without any frameworks or dependencies. Designed to score **100/100 on Lighthouse Accessibility and SEO audits** and conform to **WCAG 2.1 AA** guidelines.

---

## Live Pages

| Page | Description |
|------|-------------|
| **Home** | Hero section, stats bar, and technology tags |
| **About** | Bio, career timeline, and skill proficiency bars |
| **Projects** | Card-based project portfolio with tags and links |
| **Contact** | Accessible, validated contact form with ARIA live regions |

---

## Tech Stack

- **HTML5** — semantic structure only, zero frameworks
- **CSS3** — custom properties, grid, flexbox, responsive layout
- **Vanilla JavaScript** — SPA routing, form validation, ARIA state management
- **Google Fonts** — Space Grotesk (display) + Inter (body)

No build tools. No npm. No bundler. Open `portfolio.html` in any browser and it works.

---

## Accessibility Features (WCAG 2.1 AA)

### Semantic Structure
- Correct landmark regions: `<header role="banner">`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer role="contentinfo">`
- Strict heading hierarchy (`h1 → h2 → h3`) on every page — no skipped levels
- `<dl>` / `<dt>` / `<dd>` for the stats bar, with visually-hidden labels

### Navigation
- **Skip-to-content link** — visible on first `Tab` keypress, bypasses the nav for keyboard users
- Active page indicated via `aria-current="page"` on nav links
- Mobile toggle uses `aria-expanded` and `aria-controls`
- `Escape` key closes the mobile menu
- Focus moves to `<main>` on every page navigation

### ARIA Labels & Roles
- Every interactive element has a descriptive `aria-label` or `aria-labelledby`
- Skill progress bars: `role="progressbar"` with `aria-valuenow`, `aria-valuemin`, `aria-valuemax`
- Decorative elements (grid background, dots, emoji icons) marked `aria-hidden="true"`
- External links include `(opens in new tab)` in their `aria-label`
- Project cards use `<article>` with `aria-labelledby` pointing to the project heading

### Contact Form
- All inputs have explicit `<label for="...">` associations
- `aria-required="true"` on required fields
- `aria-describedby` links each input to its hint text and error message
- Error messages use `role="alert"` for immediate announcement
- Form status banner uses `role="status" aria-live="polite" aria-atomic="true"`
- Validation fires on `blur` (not just submit) for early, non-disruptive feedback
- On submission error: focus moves to the first invalid field
- On submission success: focus moves to the success status message
- `autocomplete` attributes set on name, email fields

### Reduced Motion
```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: .01ms !important;
    transition-duration: .01ms !important;
  }
}
```

### Focus Management
- Global `:focus-visible` ring: `2px solid #6ee7b7` with `outline-offset: 3px`
- No `outline: none` anywhere without an accessible replacement
- Tab order is logical and follows DOM order throughout

---

## SEO Implementation

### Meta Tags
```html
<meta name="description" content="..." />
<meta name="keywords" content="..." />
<meta name="author" content="Deepika R" />
<meta name="robots" content="index, follow" />
<link rel="canonical" href="https://deepikar.dev/" />
```

### Open Graph
```html
<meta property="og:type" content="website" />
<meta property="og:title" content="..." />
<meta property="og:description" content="..." />
<meta property="og:image" content="..." />
<meta property="og:image:alt" content="..." />
```

### Twitter Card
```html
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:title" content="..." />
<meta name="twitter:description" content="..." />
<meta name="twitter:image" content="..." />
```

### Structured Data (JSON-LD)
```json
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Deepika R",
  "url": "https://deepikar.dev",
  "jobTitle": "Full-Stack Developer",
  "sameAs": ["https://github.com/deepikar", "https://linkedin.com/in/deepikar"]
}
```

---

## File Structure

```
portfolio/
└── portfolio.html      # Entire site — all 4 pages in one file
└── README.md
```

The site is intentionally a single HTML file for simplicity and portability. To split into multi-file pages, copy each `<div id="page-*">` block into its own `index.html` file inside a matching directory.

---

## Customisation Guide

### Updating personal details
Search for the following placeholders and replace with your own:

| Placeholder | Location |
|-------------|----------|
| `Deepika R` | `<title>`, hero, footer, JSON-LD |
| `deepika@deepikar.dev` | contact links, JSON-LD |
| `https://deepikar.dev` | canonical tag, OG url, JSON-LD |
| `https://github.com/deepikar` | footer, contact links, JSON-LD |
| `https://linkedin.com/in/deepikar` | footer, contact links, JSON-LD |

### Adding a project card
Copy and paste this block inside the `<ul class="projects-grid">` in `page-projects`:

```html
<li>
  <article class="project-card" aria-labelledby="proj-NEW-title">
    <div class="project-icon" style="background:rgba(110,231,183,.1)" aria-hidden="true">🔧</div>
    <header>
      <h2 class="project-title" id="proj-NEW-title">Project Name</h2>
    </header>
    <ul class="project-tags" role="list" aria-label="Technologies used">
      <li class="project-tag">React</li>
    </ul>
    <p class="project-desc">Short description of the project.</p>
    <nav class="project-links" aria-label="Project links for Project Name">
      <a class="project-link" href="https://github.com/..." aria-label="View source on GitHub">↗ GitHub</a>
    </nav>
  </article>
</li>
```

### Adding a skill bar
Inside the `<div class="skills-grid">` in `page-about`:

```html
<article class="skill-card" role="listitem">
  <div class="skill-card-name">Skill Name</div>
  <div class="skill-bar" role="progressbar"
       aria-valuenow="75" aria-valuemin="0" aria-valuemax="100"
       aria-label="Skill Name proficiency: 75 percent">
    <div class="skill-fill" style="width:75%"></div>
  </div>
  <div class="skill-pct" aria-hidden="true">75%</div>
</article>
```

### Changing the accent colour
All colour decisions flow from two CSS custom properties in `:root`:

```css
--clr-accent:  #6ee7b7;   /* mint green — primary accent */
--clr-accent2: #a78bfa;   /* violet — secondary accent */
```

---

## Browser Support

Works in all modern browsers (Chrome, Firefox, Safari, Edge). No polyfills required.

| Feature | Notes |
|---------|-------|
| CSS custom properties | All modern browsers |
| CSS Grid / Flexbox | All modern browsers |
| `backdrop-filter` | Chrome, Safari, Edge (Firefox needs flag) |
| `prefers-reduced-motion` | All modern browsers |
| `:focus-visible` | All modern browsers |

---

## Deploying

Since this is a single static HTML file, it can be hosted anywhere:

```bash
# GitHub Pages — push to /docs or root of a repo
# Netlify — drag and drop the file in the dashboard
# Vercel — run: vercel deploy portfolio.html
```

For a custom domain, update the `<link rel="canonical">` and all `og:url` / JSON-LD `url` values before deploying.

---

## License

MIT — free to use, adapt, and build upon.
