# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal blog and portfolio site for kbd3v.com, built with **Astro 5** as a static site generator. Dark-themed, minimal design with TypeScript throughout.

## Commands

- `npm run dev` — Start dev server (localhost:4321)
- `npm run build` — Production build to `/dist/`
- `npm run preview` — Preview production build locally

No test framework or linter is configured.

## Architecture

**Astro 5 SSG** with file-based routing and content collections. No client-side framework — all interactivity is vanilla JS in `<script>` tags within Astro components.

### Key Files

- `src/content.config.ts` — Defines the `blog` collection schema (title, description, pubDate, updatedDate, heroImage, ogImage)
- `src/consts.ts` — Site-wide constants (SITE_TITLE, SITE_DESCRIPTION)
- `src/styles/global.css` — Design tokens as CSS custom properties and base styles
- `astro.config.mjs` — Site URL, MDX and sitemap integrations

### Content

Blog posts live in `src/content/blog/` as `.md` or `.mdx` files. Frontmatter is validated by Zod schema in `content.config.ts`. Posts route to `/blog/{id}/` via `src/pages/blog/[...slug].astro`.

Working files `_template.md` and `_guide.md` in the blog content directory are gitignored.

### Routing

File-based: `src/pages/` maps directly to URL paths. Dynamic route `[...slug].astro` handles individual blog posts using `getStaticPaths()` + `getCollection('blog')`.

### Layouts & Components

- `src/layouts/BlogPost.astro` — Blog post layout with hero image, prose styling, metadata
- `src/components/BaseHead.astro` — Global `<head>` (meta, OG tags, fonts, global CSS)
- `src/components/Header.astro` — Sticky nav with mobile hamburger menu
- `src/components/Footer.astro` — Social links

## Conventions

### Styling

- Always use CSS custom properties from `global.css` (`--color-accent`, `--color-bg`, etc.) — never hardcode colors
- Scoped `<style>` blocks in Astro components; use `:global()` for slotted/rendered markdown content
- Single responsive breakpoint: `@media (max-width: 600px)`
- Fonts: Inter (body), JetBrains Mono (code) — loaded via Google Fonts in `global.css`

### Blog Posts

Posts follow a style guide (`_guide.md`): hook, solution, features, tech stack, closing. First person, conversational tone, 300-600 words. Use `##` for sections, bold labels in lists (`- **Label:** description`). Never use em dashes. Use periods, commas, or parentheses instead.

### Images

Use Astro's `Image` component from `astro:assets` for optimization. Hero/OG images are declared as `image()` in the content schema.
