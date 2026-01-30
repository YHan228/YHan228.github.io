# Yichen Han - Personal Website

A minimalist academic portfolio built with Jekyll.

## Quick Start

```bash
bundle install
bundle exec jekyll serve
```

Site runs at `http://localhost:4000`

## Structure

```
├── _config.yml          # Site settings, author info
├── _pages/              # Static pages
│   ├── about.md         # Homepage (/)
│   ├── cv.md            # CV page
│   ├── publications.html
│   ├── teaching.html
│   └── year-archive.html # Blog listing
├── _posts/              # Blog posts (date-prefixed .md or .html)
├── _publications/       # Publication entries
├── _teaching/           # Teaching entries
├── assets/css/
│   └── custom.css       # Custom styling overrides
└── _includes/
    ├── scripts.html     # Theme toggle JS
    └── footer.html      # Simplified footer
```

## Key Files

- **`_config.yml`** - Site title, author bio, social links, collections
- **`assets/css/custom.css`** - Minimalist theme (Inter font, dark mode)
- **`_data/navigation.yml`** - Top nav menu items
- **`_includes/scripts.html`** - Dark/light theme toggle

## Adding Content

**New blog post:**
```
_posts/YYYY-MM-DD-title.md
```

**New publication:**
```
_publications/YYYY-MM-DD-title.md
```

## Styling

The site uses a minimalist black/white design with:
- Inter font
- Dark mode toggle (bottom-right corner)
- CSS variables in `custom.css` for easy theming

## Deployment

Pushes to `main` auto-deploy via GitHub Actions to GitHub Pages.

## Tech Stack

- Jekyll 3.x
- Academic Pages theme (Minimal Mistakes fork)
- GitHub Pages
