# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev          # Start dev server at localhost
npm run dev:network  # Dev server accessible over network
npm run build        # Type-check (astro check) then build
npm run preview      # Preview production build locally
npm run lint         # Run ESLint
npm run lint:fix     # Auto-fix ESLint issues
```

No test suite is configured.

## Architecture

This is an **Astro 5** static site portfolio with **Tailwind CSS** and TypeScript.

### Content Collections

All content lives in [src/content/](src/content/) as Markdown/MDX files with Zod-validated frontmatter schemas defined in [src/content/config.ts](src/content/config.ts):

- **blog/** — Posts with `title`, `description`, `date`, optional `draft`
- **projects/** — Projects with `title`, `description`, `date`, `demoURL`, `repoURL`, optional `draft`
- **work/** — Work history with `company`, `role`, `dateStart`, `dateEnd`

Entries with `draft: true` are hidden from public pages.

### Routing

File-based routing in [src/pages/](src/pages/). Collection pages use `[...slug].astro` for individual entries and `index.astro` for listings. Blog posts are grouped by year descending.

### Site Configuration

Global site metadata (name, email, socials, URLs) lives in [src/consts.ts](src/consts.ts). TypeScript types for these are in [src/types.ts](src/types.ts).

### Styling

Tailwind with class-based dark mode. Custom `animate` utility in [src/styles/global.css](src/styles/global.css) applies a fade-in + slide-up effect. Typography via `@tailwindcss/typography` for prose content.

### Path Aliases

TypeScript path aliases map `@*` to `./src/*`, so `@components/Foo.astro`, `@lib/utils`, `@consts`, etc. are all valid imports.

### Key Utilities

[src/lib/utils.ts](src/lib/utils.ts) contains `cn` (class merging), `formatDate`, `readingTime`, and `dateRange` helpers used across components.
