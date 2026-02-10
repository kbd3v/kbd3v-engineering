# AGENTS.md

> Guidance for AI coding agents working in this repository.

## Project Overview

Personal blog and portfolio at **kbd3v.com**. Astro 5 static site generator, dark theme, TypeScript throughout. No client-side framework. All interactivity is vanilla JS in `<script>` tags within Astro components.

## Commands

```bash
npm run dev        # Dev server at localhost:4321
npm run build      # Production build to /dist/
npm run preview    # Preview production build locally
```

No test framework, linter, or formatter is configured. Validate changes with `npm run build` (exit code 0 = success).

## CI/CD

GitHub Actions deploys to **GitHub Pages** on push to `main` (`.github/workflows/deploy.yml`). Node 20, `npm ci`, `npm run build`, uploads `./dist/` as Pages artifact. Do not modify the workflow without explicit approval.

## Architecture

**Astro 5 SSG** with file-based routing and content collections.

```
src/
  components/     # Astro components (BaseHead, Header, Footer, Logo, etc.)
  content/
    blog/         # Blog posts as .md/.mdx (frontmatter validated by Zod)
  layouts/        # BlogPost.astro (single layout)
  pages/          # File-based routing (index, blog/, about, projects)
  styles/         # global.css (design tokens + base styles)
  consts.ts       # SITE_TITLE, SITE_DESCRIPTION
  content.config.ts  # Blog collection schema
astro.config.mjs  # Site URL, MDX + sitemap integrations
```

### Key Patterns

- **Routing**: `src/pages/` maps to URLs. Dynamic route `[...slug].astro` handles blog posts via `getStaticPaths()` + `getCollection('blog')`.
- **Content**: Blog posts in `src/content/blog/` as `.md`/`.mdx`. Files prefixed with `_` are gitignored working files (templates, guides).
- **Frontmatter schema** (in `content.config.ts`): `title`, `description`, `pubDate`, `updatedDate?`, `heroImage?`, `ogImage?`.
- **No client framework**: Interactive behavior uses vanilla JS in `<script>` tags (see Header.astro, projects.astro).

## TypeScript

- Config extends `astro/tsconfigs/strict` with `strictNullChecks: true`.
- ESM only (`"type": "module"` in package.json).
- Use `type` keyword for type-only imports: `import type { CollectionEntry } from 'astro:content'`.
- Use inline `type` in mixed imports: `import { type CollectionEntry, getCollection } from 'astro:content'`.
- Define component props with `interface Props` or `type Props = ...` in the frontmatter.
- Never use `as any`, `@ts-ignore`, or `@ts-expect-error`.

## Code Style

### Astro Component Frontmatter

Import order (group with blank lines between):
1. Local component/module imports (relative paths).
2. Astro module imports (`astro:content`, `astro:assets`).
3. Constant imports (`../consts`).
4. Logic (data fetching, transformations).

**Example** (from `[...slug].astro`):
```astro
---
import { type CollectionEntry, getCollection, render } from 'astro:content';
import BlogPost from '../../layouts/BlogPost.astro';

export async function getStaticPaths() {
  const posts = await getCollection('blog');
  return posts.map((post) => ({
    params: { slug: post.id },
    props: post,
  }));
}
type Props = CollectionEntry<'blog'>;

const post = Astro.props;
const { Content } = await render(post);
---
```

### Formatting

- **Indentation**: Tabs in Astro/HTML/CSS (Astro default).
- **Quotes**: Single quotes in JS/TS, double quotes in HTML attributes.
- **Semicolons**: Always.
- **Trailing commas**: Yes, in arrays and object literals.
- **Arrow functions**: Preferred for callbacks and short expressions.
- **Template literals**: Use for string interpolation (`` `/blog/${post.id}/` ``).

### Naming

- **Files**: kebab-case for pages and content (`[...slug].astro`, `tidwerk.md`). PascalCase for components (`BaseHead.astro`, `FormattedDate.astro`).
- **Variables**: camelCase (`canonicalURL`, `typeColors`, `imageSrc`).
- **Constants**: UPPER_SNAKE_CASE for site-wide constants (`SITE_TITLE`, `SITE_DESCRIPTION`).
- **CSS classes**: kebab-case (`hero-image`, `post-link`, `tech-pill`).
- **Types**: PascalCase (`Props`, `CollectionEntry`).

## CSS & Styling

### Design Tokens (from `global.css`)

Always use CSS custom properties. Never hardcode colors.

```css
--color-bg: #0f172a;        --color-bg-alt: #1e293b;
--color-text-main: #e2e8f0; --color-text-muted: #94a3b8;
--color-accent: #8b5cf6;    --color-accent-glow: rgba(139, 92, 246, 0.3);
--color-border: #334155;
--font-body: 'Inter', system-ui, -apple-system, sans-serif;
--font-mono: 'JetBrains Mono', monospace;
--max-width: 800px;          --radius: 8px;
```

### Rules

- **Scoped styles**: Use `<style>` blocks in Astro components (scoped by default).
- **Global overrides**: Use `:global()` for slotted/rendered markdown content (see `BlogPost.astro` `.prose :global(p)`).
- **Responsive breakpoint**: `@media (max-width: 600px)` is the single breakpoint used throughout.
- **Transitions**: `transition: 0.2s ease` is the standard. Use `color`, `border-color`, `transform` transitions.
- **Border radius**: Use `var(--radius)` for standard rounding, `50%` for circles, `999px` for pills.

## Images

Use Astro's `Image` component from `astro:assets` for optimization. Hero/OG images are declared as `image()` in the content schema.

```astro
import { Image } from 'astro:assets';
<Image width={720} height={360} src={post.data.heroImage} alt="" />
```

## Blog Posts

Posts live in `src/content/blog/` as `.md` or `.mdx`.

### Writing Style

- First person, conversational tone with a touch of humor and realness.
- 300-600 words. Structure: hook, solution, features, tech stack, closing.
- Use `##` for sections, bold labels in lists (`- **Label:** description`).
- **Never use em dashes**. Use periods, commas, or parentheses instead.

### Frontmatter Template

```yaml
---
title: "Post Title"
description: "A brief description for SEO and previews."
pubDate: "2026-01-15"
heroImage: ./hero.png    # optional
ogImage: ./og.png        # optional
---
```

## Page Structure

Every page follows this structure:

```astro
<!doctype html>
<html lang="en">
  <head>
    <BaseHead title={...} description={...} />
    <style>/* scoped styles */</style>
  </head>
  <body>
    <Header />
    <main>
      <!-- page content -->
    </main>
    <Footer />
  </body>
</html>
```

## Dependencies

Minimal dependency footprint. Only Astro core + official integrations:

- `astro` (core), `@astrojs/mdx`, `@astrojs/rss`, `@astrojs/sitemap`, `sharp` (image optimization).

Do not add new dependencies without explicit approval.
