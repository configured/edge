# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an **Adobe Experience Manager (AEM) Edge Delivery Services** project based on the AEM Boilerplate. It's a lightweight, performance-focused website framework that uses:

- **Block-based architecture** for components
- **Edge-first delivery** with optimized content loading
- **JavaScript modules** for functionality
- **CSS** for styling without frameworks

## Development Commands

### Linting and Code Quality
```bash
# Run all linting (JS + CSS)
npm run lint

# Lint JavaScript only
npm run lint:js

# Lint CSS only
npm run lint:css
```

### Local Development
```bash
# Install dependencies
npm i

# Start local development server
aem up
```

The development server runs on `http://localhost:3000` using the AEM CLI.

### Testing
Check for test runner configuration - this project uses `@web/test-runner` for testing.

## Architecture

### Core Files
- `scripts/aem.js` - Main AEM utility functions and block management
- `scripts/scripts.js` - Project-specific initialization and auto-block builders
- `scripts/delayed.js` - Delayed loading functionality
- `fstab.yaml` - Mountpoint configuration for content sources

### Block System
Blocks are located in `/blocks/` with each block having:
- `{blockname}.js` - Block functionality
- `{blockname}.css` - Block styling

**Available blocks:**
- `header` - Navigation and site header
- `footer` - Site footer
- `cards` - Card-based content display
- `columns` - Column layouts
- `hero` - Hero sections
- `code` - Code syntax highlighting

### Auto-Generated Blocks
The system automatically creates blocks from content:
- **Hero blocks** - Auto-generated from H1 + picture combinations
- **Code blocks** - Auto-generated from `<pre>` elements with language indicators

### Content Loading Strategy
The project uses a three-phase loading approach:
1. **Eager loading** (`loadEager`) - Critical path to LCP
2. **Lazy loading** (`loadLazy`) - Non-critical content after LCP
3. **Delayed loading** (`loadDelayed`) - Background functionality after 3 seconds

### Block Development
When creating or modifying blocks:
- Follow the existing pattern in `/blocks/`
- Export a default function that decorates the block element
- Use `createOptimizedPicture()` for images
- Leverage AEM utilities from `scripts/aem.js`

### Styling
- `styles/styles.css` - Global styles
- `styles/fonts.css` - Font loading
- `styles/lazy-styles.css` - Lazy-loaded styles
- Block-specific CSS in respective block folders

### Content Management
- Content is sourced from Google Drive (see `fstab.yaml`)
- Content is fetched as plain HTML and processed into blocks
- Navigation content is loaded from `/nav.plain.html`

## Key AEM Utilities

Import from `scripts/aem.js`:
- `buildBlock()` - Create block elements
- `decorateIcons()` - Process icon spans
- `createOptimizedPicture()` - Generate responsive images
- `loadCSS()` - Dynamic CSS loading
- `getMetadata()` - Access page metadata
- `readBlockConfig()` - Parse block configuration