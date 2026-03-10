# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal portfolio and blog website built with Astro, deployed on Railway.

## Commands

- **Dev server**: `pnpm dev`
- **Build** (type-check + build): `pnpm build`
- **Preview production build**: `pnpm preview`
- **Format**: `npx prettier --write .` (uses prettier-plugin-astro)

No test runner is configured.

## Architecture

**Framework**: Astro 5 with static output mode and `@astrojs/node` standalone adapter (deployed on Railway).
**Interactive islands**: Solid.js (configured as JSX import source in tsconfig).
**Styling**: Scoped CSS in Astro `<style>` tags with CSS custom properties — no Tailwind.

### Source Structure

- `src/pages/` — File-based routing. Blog uses dynamic `[...slug].astro` route.
- `src/blocks/` — Large page sections (Hero, About, Experience, Portfolio). These are assembled in page files.
- `src/components/` — Reusable UI (Navbar, Footer, Card, Button, Link, etc.).
- `src/layouts/` — `MainLayout` (global wrapper with theme support) and `BlogPostLayout`.
- `src/content/` — Astro Content Collections. Blog posts are Markdown with typed frontmatter schema in `config.ts`.
- `src/icons/` — SVG icon assets used alongside `astro-icon` (Iconify sets: carbon, devicon, skill-icons).

### Key Patterns

- **Theming**: Dark/light mode via `theme-${theme}` CSS class on body. Colors defined as CSS custom properties in MainLayout.
- **Animations**: Scroll-reveal via Intersection Observer API. Smooth transitions with `cubic-bezier` timing.
- **Typography**: Fluid sizing with `clamp()`.
- **Blog content schema**: Posts have `title`, `pubDate`, `description`, `tags`, `thumbnail`, `videoId`, `videoDescription`, and `types` (guia-escrita | guia-video).
- **Email**: Uses `resend` package for contact form (serverless endpoint).

## Code Style

- Prettier with single quotes, 120 char width, ES5 trailing commas
- TypeScript strict mode (extends `astro/tsconfigs/strict`)
