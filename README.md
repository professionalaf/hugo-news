# Hugo News Theme

A modern, responsive Hugo theme designed for news and media websites. Built with Tailwind CSS and Alpine.js.

![Hugo News Theme Screenshot](https://raw.githubusercontent.com/professionalaf/hugo-news/main/images/screenshot.png)

## Features

- 🎨 Modern design with Tailwind CSS
- 🔍 Built-in search functionality
- 📱 Fully responsive
- 🏷️ Support for categories, tags, and authors
- 🖼️ Featured articles with large images
- 🔄 Dynamic category browsing
- 👥 Author profiles
- 🔍 Search functionality with Fuse.js
- ⚡ Fast loading with minimal JavaScript
- 🎨 Clean typography and spacing
- 📊 Google Analytics 4 integration

## Installation

### For Hugo Site Users

1. In your Hugo site directory, run:
```bash
git submodule add https://github.com/professionalaf/hugo-news themes/hugo-news
```

2. Install theme dependencies (required for CSS/JS processing):
```bash
cd themes/hugo-news
npm install
```

3. Update your `hugo.toml` configuration:
```toml
theme = "hugo-news"
```

**Note**: This theme requires Hugo Extended version 0.128.0 or higher for PostCSS support.

## Configuration

### Google Analytics
The theme includes built-in support for Google Analytics 4 (GA4). To enable tracking:

1. Get your GA4 Measurement ID from your Google Analytics account (format: G-XXXXXXXXXX)
2. Add it to your site's config file:

```toml
googleAnalytics = "G-XXXXXXXXXX"  # Replace with your GA4 measurement ID
```

The analytics code will:
- Only load when a valid measurement ID is provided
- Respect user privacy settings and cookie consent
- Load asynchronously to not impact page performance
- Track page views and basic user interactions

If you don't want analytics, simply leave the googleAnalytics parameter commented out:
```toml
# googleAnalytics = "G-MEASUREMENT_ID"
```

### Basic Configuration

Example `hugo.toml` configuration:

```toml
baseURL = 'https://example.org/'
languageCode = 'en-US'
title = 'My Hugo News Site'

[taxonomies]
  category = "categories"
  tag = "tags"
  author = "authors"

[outputs]
  home = ["HTML", "RSS", "JSON"]

[[menus.main]]
name = "Home"
url = "/"
weight = 10

[[menus.main]]
name = "Categories"
url = "/categories"
weight = 20

[[menus.main]]
name = "Tags"
url = "/tags"
weight = 30
```

## Content Structure

```
content/
├── _index.md
├── articles/
│   ├── first-post.md
│   └── second-post.md
├── authors/
│   ├── _index.md
│   └── john-doe/
│       ├── _index.md
│       └── avatar.jpg
└── categories/
    └── _index.md
```

### Article Front Matter

```yaml
---
title: "Article Title"
date: 2024-01-01
author: "Author Name"
categories: ["Category1", "Category2"]
tags: ["tag1", "tag2"]
featured_image: "path/to/image.jpg"
description: "Article description"
---
```

### Author Front Matter

```yaml
---
title: "Author Name"
bio: "Author biography"
avatar: "author-image.jpg"
social:
  twitter: "twitterhandle"
  linkedin: "linkedinprofile"
---
```

## Comments System

The theme includes two types of comment systems:

### Static Comments

Static comments are stored alongside the article content in a `comments.json` file. They are visible to all users and persist across sessions. To add static comments:

1. Create a `comments.json` file in your article's directory (next to your article's markdown file)
2. Use this structure:
```json
{
  "comments": [
    {
      "name": "Author Name",
      "content": "Comment text",
      "date": "2024-01-11T15:30:00Z",
      "isStatic": true
    }
  ]
}
```

Example directory structure:
```
content/
└── articles/
    └── my-article/
        ├── index.md
        ├── featured-image.jpg
        └── comments.json
```

### Dynamic Comments

Dynamic comments are stored in the user's browser localStorage. These comments:
- Only visible to the user who created them
- Persist across page refreshes but only in the same browser
- Are not shared with other users
- Will be cleared if the user clears their browser data

Dynamic comments are automatically handled by the theme's JavaScript and don't require any setup.

## Development

### Requirements

- Hugo Extended Version (>= 0.128.0) - Required for PostCSS integration
- Node.js (>= 18.0.0) - Required for Tailwind CSS and PostCSS processing

### Setup

1. Clone the repository:
```bash
git clone https://github.com/professionalaf/hugo-news.git
cd hugo-news
```

2. Install dependencies:
```bash
npm install
```

### Development Workflow

1. **Start development server** (runs from exampleSite):
```bash
npm run dev
```

This will start Hugo's development server with hot reload. The server will automatically process CSS through PostCSS and Tailwind CSS.

2. **Build for production**:
```bash
npm run build
```

3. **Test the theme** (builds exampleSite):
```bash
npm test
```

### Build Process

The theme uses Hugo's built-in asset pipeline:

- **CSS**: Processed through PostCSS with Tailwind CSS and Autoprefixer
  - Source: `assets/css/main.css`
  - Automatically minified and fingerprinted in production
  - Tailwind CSS classes are purged based on usage in templates

- **JavaScript**: Alpine.js is bundled via Hugo's asset pipeline
  - Source: `assets/js/alpine.js`
  - Automatically minified and fingerprinted in production

- **Configuration**:
  - `tailwind.config.js` - Tailwind CSS configuration
  - `postcss.config.js` - PostCSS plugins (Tailwind, Autoprefixer)
  - `hugo.toml` - Hugo build configuration with cache busters

### Testing

The theme includes automated testing via GitHub Actions:

- Builds with multiple Hugo versions (0.128.0 minimum, latest)
- Validates HTML output
- Checks CSS and JS asset generation
- Runs on every push and pull request

To test locally:
```bash
npm test
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

Released under the [MIT License](LICENSE).

## Credits

- Built with [Tailwind CSS](https://tailwindcss.com/)
- Interactive components powered by [Alpine.js](https://alpinejs.dev/)
- Search functionality using [Fuse.js](https://fusejs.io/)
