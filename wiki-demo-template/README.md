# wiki-demo

A wiki encyclopedia website built with Jekyll. Uses Markdown to generate clean, well-organized wiki pages.

## Features

- 📚 Wiki articles organized by categories
- 🔗 Sidebar navigation auto-generated from article metadata
- 📝 Markdown-based content with code syntax highlighting
- 📱 Responsive layout (desktop + mobile)
- 🏷️ Article tags and related articles
- 🔍 Category browsing page
- ⚡ Fast static site — no server required

## Project Structure

```
wiki-demo/
├── _config.yml          # Site configuration
├── _layouts/            # Page layouts
│   ├── default.html     # Main layout with sidebar
│   ├── wiki.html        # Wiki article layout
│   └── page.html        # Simple page layout
├── _includes/           # Reusable HTML snippets
│   ├── sidebar.html     # Auto-generated navigation
│   ├── meta.html        # HTML meta tags
│   └── analytics.html   # Analytics snippet
├── _sass/               # SCSS stylesheets
│   ├── _variables.scss  # Colors and breakpoints
│   ├── _reset.scss      # CSS reset
│   └── _highlights.scss # Code syntax highlighting
├── _wiki/               # Wiki articles (Markdown)
│   ├── overview.md
│   ├── getting-started.md
│   ├── features.md
│   ├── configuration.md
│   ├── api-reference.md
│   ├── faq.md
│   └── changelog.md
├── images/              # Site images
├── style.scss           # Main stylesheet
├── index.html           # Home page
├── categories.md        # Categories listing
├── about.md             # About page
└── 404.md               # 404 error page
```

## Adding Wiki Articles

Create a new Markdown file in `_wiki/`:

```markdown
---
title: "Your Article Title"
description: "Brief description shown in listings"
category: "Category Name"
order: 1                    # Sort order within category
last_updated: "2024-01-01"
toc: true                   # Show table of contents
tags: [tag1, tag2]
related:
  - Another Article Title
---

## Section One

Your content here...
```

### Front Matter Fields

| Field | Type | Description |
|-------|------|-------------|
| `title` | string | Article title (required) |
| `description` | string | Short description |
| `category` | string | Category name for grouping |
| `category_icon` | string | Emoji icon for the category |
| `category_description` | string | Category description for home page |
| `order` | number | Sort order within category |
| `last_updated` | date | Last update date (YYYY-MM-DD) |
| `toc` | boolean | Show table of contents (default: true) |
| `tags` | list | Article tags |
| `related` | list | Related article titles |

## Local Development

### Requirements

- Ruby 2.7+
- Jekyll 4.x
- Bundler

### Setup

```bash
gem install bundler jekyll
bundle install
bundle exec jekyll serve
```

Open `http://localhost:4000` in your browser.

### With Docker

```bash
docker run --rm -v "$PWD:/srv/jekyll" -p 4000:4000 jekyll/jekyll jekyll serve
```

## Deployment

### GitHub Pages

1. Push to your GitHub repository
2. Go to **Settings → Pages**
3. Set source to the `main` branch
4. Your site will be live at `https://username.github.io/wiki-demo`

### Custom Domain

Add a `CNAME` file with your domain name:

```
wiki.yourdomain.com
```

Then configure your DNS provider to point to GitHub Pages.

## Customization

### Site Name and Description

Edit `_config.yml`:

```yaml
name: "Your Wiki Name"
description: "Your wiki description"
avatar: /images/your-logo.png
```

### Colors and Theme

Edit `_sass/_variables.scss` to change the color scheme:

```scss
$primary: #2563eb;        // Primary blue
$header-bg: #1e293b;      // Dark header
$sidebar-bg: #f8fafc;     // Light sidebar
```

## License

MIT License — see [LICENSE](LICENSE) for details.
