# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

### Essential Commands
- `npm run dev` - Start development server (alias: `npm run start`)
- `npm run build` - Type check and build for production (`astro check && astro build`)
- `npm run preview` - Preview built site locally
- `npm run format` - Format code with Prettier
- `npm run generate-ogp` - Generate Open Graph images using custom tool

### Requirements
Before development, create `.env` file with:
```env
MICROCMS_SERVICE_DOMAIN="{ microCMS domain }"
MICROCMS_API_KEY="{ microCMS API KEY }"
BUN_VERSION="{ Bun version }"
BASE_URL="{ Page URL }"
```

## Architecture Overview

### Content Management
This is a **hybrid content system**:
- **microCMS**: Headless CMS for dynamic blog content (primary source)
- **Local Markdown**: Static content and pages (backup/fallback)
- **Content Collections**: Astro's type-safe content validation with Zod schemas

Blog posts are fetched from microCMS API but can fall back to local markdown files in `/src/content/` if needed.

### Key Directories
- `/src/pages/` - Route-based pages:
  - `index.astro` - Homepage with 3D globe (Cobe library)
  - `blog/[...page].astro` - Paginated blog listing (12 posts per page)
  - `blog/[...slug].astro` - Individual blog post pages
  - `about.mdx` - About page
  - `rss.xml.js` - RSS feed generation
- `/src/components/` - Reusable Astro and React components
- `/src/layouts/` - Page layout templates
- `/src/library/` - Utility functions and microCMS API client
- `/tools/generate-ogp/` - Custom OGP image generation tool

### TypeScript Path Aliases
- `@components/*` → `src/components/*`
- `@layouts/*` → `src/layouts/*`
- `@library/*` → `src/library/*`
- `@pages/*` → `src/pages/*`
- `@hooks/*` → `src/hooks/*`
- `@styles/*` → `src/styles/*`
- `@consts` → `src/consts.ts`

### Key Technologies
- **Astro 5.5.5** - Static site generator with React integration
- **microCMS JS SDK** - Headless CMS client
- **React 18.3.1** - Interactive components (GlobalMusicPlayer, etc.)
- **TypeScript** - Strict configuration with path aliases
- **Cobe** - 3D globe visualization on homepage
- **Howler.js** - Audio player functionality

### Special Features
- **PWA Support** - Full PWA configuration with service worker and caching strategies
- **Image Optimization** - Multiple formats (AVIF, WebP, JPEG) with responsive loading
- **Performance** - CSS purging, font subsetting, lazy loading
- **OGP Generation** - Custom tool using @vercel/og for social media previews

### Content Structure
Blog posts support:
- Multiple writers/authors
- Tag categorization  
- Table of contents generation (Tocbot)
- Social sharing functionality
- Pagination (12 posts per page)

### Build Configuration
- Static output (`output: "static"`)
- PostCSS with Autoprefixer
- CSS purging via astro-purgecss
- Sitemap and robots.txt generation
- Node.js 20.10.0 (Volta configuration)