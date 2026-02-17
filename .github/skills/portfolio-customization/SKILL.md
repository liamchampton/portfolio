---
name: portfolio-customization
description: 'Add, edit, or remove content on this personal portfolio website. Use for: adding a new video card, project card, conference talk, or blog post; updating view counts; reordering cards; changing hero text, highlights, or social links; updating meta/OG tags; hiding or showing cards in the expand section.'
argument-hint: 'Describe what you want to add or change (e.g. "add a new video card for https://youtu.be/...")'
---

# Portfolio Customization

## Site Structure

```
index.html        — All content (single-page)
stylesheet.css    — All styles (design tokens at top)
assets/           — profile-picture.jpeg, copilot-logo.svg
```

The site is a single HTML page with four vertical sections, each full-viewport height:
1. **Hero** — photo, name, tagline, highlights, social links
2. **Recent Projects** (`#projects`) — tech project cards with tags
3. **Recent Video Content** (`#videos`) — YouTube video cards, 3-column grid
4. **Conference & Meetup Talks** (`#conferences`) — talk cards with dates
5. **Blogs** (`#blogs`) — article link cards

---

## Card Visibility: Shown vs Hidden

Each section shows **2 rows** of cards by default. Cards beyond the second row use `class="card hidden-card"` and are revealed by a "Show More" button.

- **Visible card**: `<article class="card">`
- **Hidden card**: `<article class="card hidden-card">`
- **Featured card** (purple top border): add `featured` class → `<article class="card featured">`
- **CTA card** (channel/blog link): `<article class="card cta-card hidden-card">`

The videos grid is **3 columns**, so rows 1–2 = cards 1–6 visible.  
The projects/conferences grid is **auto-fill (min 320px)**, typically 3 columns on desktop.

Always keep the CTA card last and hidden.

---

## Adding a Video Card

Paste inside `<div class="card-grid" id="videos-grid">`, before the CTA card.  
Add `hidden-card` if it would appear on row 3+.

```html
<article class="card">
    <div class="card-content">
        <i class="fab fa-youtube card-icon"></i>
        <h3 class="card-title">Your Video Title Here</h3>
        <p class="card-description">Short description of the video content.</p>
        <span class="video-views"><i class="fas fa-eye"></i> 10k+ views</span>
        <a href="https://youtu.be/VIDEO_ID" class="card-link" target="_blank" rel="noopener noreferrer">
            <i class="fab fa-youtube"></i> Watch Now <i class="fas fa-play"></i>
        </a>
    </div>
</article>
```

- **Order**: newest first (top-left)
- Omit the `video-views` span if the count isn't known yet
- Use the full YouTube URL for live streams: `https://www.youtube.com/live/VIDEO_ID`

---

## Adding a Project Card

Paste inside `<div class="card-grid">` under `#projects`.

```html
<article class="card">
    <div class="card-content">
        <div class="card-tags">
            <span class="tag">Go</span>
            <span class="tag">Azure</span>
        </div>
        <h3 class="card-title">Project Name</h3>
        <p class="card-description">What this project does and why it's interesting.</p>
        <a href="https://github.com/username/repo" class="card-link" target="_blank" rel="noopener noreferrer">
            <i class="fab fa-github"></i> View Repository <i class="fas fa-arrow-right"></i>
        </a>
    </div>
</article>
```

If no public repo exists yet, replace the link with:
```html
<span class="no-recording"><em>Public repository coming soon...</em></span>
```

---

## Adding a Conference / Meetup Talk

Paste inside `<div class="card-grid" id="talks-grid">`, before the CTA card.  
Add `hidden-card` if beyond row 2. Add `featured` for keynotes/major conferences.

```html
<article class="card featured">
    <div class="card-content">
        <span class="card-date">Month YYYY</span>
        <h3 class="card-title">Conference Name</h3>
        <h4 class="card-subtitle">Session Type (Keynote / Breakout / Workshop)</h4>
        <p class="card-description">Brief summary of what was delivered.</p>
        <!-- If a recording exists: -->
        <a href="https://youtu.be/VIDEO_ID" class="card-link" target="_blank" rel="noopener noreferrer">
            <i class="fab fa-youtube"></i> Watch Now <i class="fas fa-play"></i>
        </a>
        <!-- If no recording: -->
        <span class="no-recording"><i class="fas fa-times-circle"></i> <em>No recording available</em></span>
    </div>
</article>
```

---

## Adding a Blog Post

Paste inside `<div class="card-grid">` under `#blogs`, before the CTA card.

```html
<article class="card">
    <div class="card-content">
        <i class="fas fa-pen-nib card-icon"></i>
        <h3 class="card-title">Article Title</h3>
        <a href="https://dev.to/username/article-slug" class="card-link" target="_blank" rel="noopener noreferrer">
            Read Article <i class="fas fa-arrow-right"></i>
        </a>
    </div>
</article>
```

Good icon choices: `fa-terminal`, `fa-code-compare`, `fa-pen-nib`, `fab fa-github`, `fas fa-cloud`

---

## Updating Hero Content

**Name / tagline**: edit `<h1>` and `<p class="tagline">` directly.

**Highlight chips** (the pill badges):
```html
<span class="highlight"><i class="fas fa-building"></i> Your Company</span>
```

**Social links**: update `href` on `.social-btn` anchors. Supported styles: `github`, `twitter`, `linkedin`.

**Profile photo**: replace `./assets/profile-picture.jpeg` (keep filename or update the `src`).

---

## Updating Meta / SEO Tags

At the top of `<head>`, update these five values consistently:

| Tag | What to change |
|-----|---------------|
| `<title>` | Your name and role |
| `<meta name="description">` | 1–2 sentence bio |
| `og:url` | Your deployed URL |
| `og:image` / `twitter:image` | Absolute URL to your profile photo |
| `twitter:site` | Your Twitter/X handle |

---

## Design Tokens (Colors & Spacing)

All visual values live in `:root` at the top of `stylesheet.css`. Key tokens:

| Token | Default | Purpose |
|-------|---------|---------|
| `--color-accent-primary` | `#7c3aed` | Purple accent, borders, hover |
| `--color-bg-primary` | `#0f0f1a` | Page background |
| `--color-bg-card` | `#16213e` | Card background |
| `--color-text-primary` | `#f8fafc` | Main text |
| `--color-text-secondary` | `#94a3b8` | Subtitles, labels |

Change `--color-accent-primary` and `--color-accent-secondary` to rebrand the whole site.

---

## Rules to Follow

- All external links **must** include `target="_blank" rel="noopener noreferrer"`
- Videos section: keep to **6 visible cards** (2 rows × 3 columns); mark extras `hidden-card`
- Always place the CTA card **last** in its grid and mark it `hidden-card`
- Newest content goes **first** (top-left) within each section
- Do **not** add inline styles — use existing CSS custom properties or classes
