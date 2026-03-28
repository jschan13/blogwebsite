# The Meridian — Handoff Guide

## What You've Received

Two HTML files that work together as a complete blog system:

| File | Purpose |
|------|---------|
| `index.html` | Your public website (Home, Blog, About, Contact, Articles) |
| `admin.html` | Your content management panel |

Both files work by simply opening them in a browser. No server, no installation required.

---

## Deploying Your Site

### Recommended: Netlify (Free, 5 minutes)
1. Go to [netlify.com](https://netlify.com) and sign up free
2. Drag both files into the Netlify deploy area
3. Your site goes live instantly at a `*.netlify.app` URL
4. Connect a custom domain in Settings → Domain Management

### Alternative: GitHub Pages
1. Create a free GitHub account and a new repository
2. Upload both files
3. Go to Settings → Pages → Enable from `main` branch
4. Live at `yourusername.github.io/reponame`

---

## Adding New Blog Posts

The site currently uses a JavaScript data object to store articles. To add a new post:

### Step 1: Open `index.html` in a code editor
(VS Code is free and excellent: [code.visualstudio.com](https://code.visualstudio.com))

### Step 2: Find the ARTICLES object
Search for `const ARTICLES = {` — it's around line 600.

### Step 3: Add your post
Copy this template and paste it inside the `ARTICLES` object (before the closing `}`):

```javascript
your_slug: {
  tag: 'Culture',           // Category label
  readTime: '6 min',        // Estimated reading time
  title: 'Your Article Title',
  deck: 'One compelling sentence that summarises the piece.',
  author: 'Your Name',
  initials: 'YN',           // 2 letters for avatar
  date: 'April 1, 2025',
  imgClass: 'art-1',        // art-1 through art-6 for cover style
  body: `
    <p>Your first paragraph here.</p>
    <h2>A Section Heading</h2>
    <p>More content here.</p>
    <blockquote>A pull quote or key insight.</blockquote>
    <p>Closing paragraph.</p>
  `,
  tags: ['Culture', 'Media']
},
```

### Step 4: Add to the post list
Find `const ALL_POSTS = [` and add:
```javascript
{slug:'your_slug', tag:'culture', category:'culture'},
```

### Step 5: Save and re-upload to Netlify

---

## Using the Admin Panel (`admin.html`)

The admin panel gives you a visual interface:

- **Dashboard** — overview of all posts and recent activity
- **All Posts** — filter, search, edit, or delete articles
- **New Post / Editor** — write with formatting toolbar, set metadata, upload cover image, add tags
- **Media Library** — browse uploaded images
- **Site Settings** — update site name, newsletter API, SEO defaults

> **Note:** The admin panel in this version is a UI prototype. To make it fully "save to live site", you have two options:
> 1. **Simple**: Use it as a writing interface, then manually copy the content into `index.html`
> 2. **Fully automated**: Connect to a backend (see CMS options below)

---

## Upgrading to a Real CMS (Optional)

When you're ready to manage everything without touching code, these are the best options:

### Netlify CMS (Free, no backend needed)
- Adds a `/admin` route to your Netlify site
- Full visual editor with media uploads
- Changes commit directly to GitHub
- Setup time: ~30 minutes
- Guide: [decapcms.org/docs](https://decapcms.org/docs)

### Ghost (Self-hosted or $9/mo hosted)
- Purpose-built blogging platform
- Beautiful editor, newsletter built-in, paid subscriptions
- Export your current posts as JSON
- Best if you want a serious publishing business
- [ghost.org](https://ghost.org)

### WordPress (Self-hosted ~$5/mo)
- Maximum flexibility, thousands of themes
- Large ecosystem of plugins
- Familiar to most freelancers and developers
- Best if you want maximum plugin support

---

## Customising the Design

All design tokens (colours, fonts, spacing) are defined at the top of `index.html` in the `:root { }` block:

```css
:root {
  --ink:        #0f0f0f;   /* Main text colour */
  --paper:      #faf8f4;   /* Background */
  --accent:     #1a5c3a;   /* Green accent — change this to rebrand */
  --ff-display: 'Playfair Display', Georgia, serif;  /* Headline font */
  --ff-body:    'Source Serif 4', Georgia, serif;    /* Body font */
}
```

**To change the accent colour**: replace `#1a5c3a` and `#2d7a52` with your preferred colour.

**To change fonts**: Replace the Google Fonts `<link>` tag and update the `--ff-display` and `--ff-body` variables.

---

## Responsive Breakpoints

The site adapts at these breakpoints:

| Breakpoint | Layout |
|-----------|--------|
| > 900px | Full desktop: 3-column grid, hero with sidebar |
| 721–900px | Tablet: 2-column grid |
| ≤ 720px | Mobile: single column, hamburger menu |
| ≤ 480px | Small mobile: stacked newsletter form |

---

## Browser Support

Tested and working in:
- Chrome / Edge 90+
- Firefox 88+
- Safari 14+
- Mobile Safari (iOS 14+)
- Chrome for Android

---

## Editing the About and Contact Pages

Both pages are inside `index.html`. Search for:
- `id="page-about"` — edit team bios, mission text, values
- `id="page-contact"` — edit contact info items in `.info-item` divs

---

## Performance Notes

- Fonts load from Google Fonts CDN (2 requests, cached after first visit)
- No JavaScript frameworks — pure vanilla JS (~8KB)
- No external CSS libraries
- SVG illustrations are inline (zero HTTP requests)
- Target load time on 3G: under 2 seconds

---

*Questions? Email: editorial@meridian.pub*
