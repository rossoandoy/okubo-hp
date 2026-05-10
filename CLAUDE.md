# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Structure

This is a parent repository containing project documentation and two git submodules:

- **`professor-s-keio-portal/`** — Main site for Professor Okubo's Keio portal (active development)
- **`okubo-personal-page/`** — Personal page (separate project, uses pnpm + Express backend)
- Root contains Japanese-language planning documents (企画書, 仕様書, 手順書) and implementation records

Clone with submodules: `git clone --recurse-submodules <URL>`
If submodules are empty: `git submodule update --init --recursive`

## professor-s-keio-portal (Main Project)

### Commands

```bash
cd professor-s-keio-portal
npm ci                    # Install dependencies
npm run dev               # Dev server on port 8080
npm run build             # Production build → dist/
npm run build:keio        # Build + generate Keio server fallbacks
npm run lint              # ESLint
npm run test              # Vitest (run once)
npm run test:watch        # Vitest (watch mode)
npm run preview           # Preview production build
npm run check:paths       # Check for non-ASCII file paths
npm run check:links       # Check internal links
```

### Tech Stack

- **React 18** + **TypeScript** + **Vite 5** (SWC plugin)
- **React Router v6** for client-side routing
- **Tailwind CSS 3** + **shadcn/ui** (Radix UI primitives in `src/components/ui/`)
- **TanStack React Query** for data fetching
- **Framer Motion** for animations
- **Vitest** + **Testing Library** for tests
- **Lovable** was used for initial scaffolding (lovable-tagger in dev deps)

### Architecture

Single-page app with these routes defined in `src/App.tsx`:
- `/` — Landing page (Hero → Research → Publications → Career → Contact sections)
- `/by-topic` — Publications browser with search
- `/publications/:slug` — Publication detail
- `/research/:topicSlug` — Research theme detail
- `/research-agenda` — Research agenda
- `/policy`, `/news`, `/sitemap` — Static-ish pages

Key patterns:
- **Path alias**: `@/` maps to `src/` (configured in `vite.config.ts` and `tsconfig.json`)
- **Base path**: Controlled via `VITE_BASE_PATH` env var for GitHub Pages deployment (e.g., `/professor-s-keio-portal/`). `BrowserRouter` reads `import.meta.env.BASE_URL`.
- **Content loading**: `src/lib/contentLoader.ts` handles data fetching
- **Section components**: Top page sections are standalone components in `src/components/` (HeroSection, ResearchSection, PublicationsSection, CareerSection, ContactSection)
- **Navigation**: `src/components/Navigation.tsx` — nav items link to top-page anchors (`/#research`, `/#career`, `/#contact`) or routes (`/by-topic`)

### CI/CD (GitHub Actions)

- **`pr-check.yml`** — Runs on PR: install, build, lint, quality checks
- **`build-release.yml`** — On main merge: build + ZIP artifact for deployment
- **`deploy-pages.yml`** — On main push: build and deploy to GitHub Pages

### Deployment

- **GitHub Pages**: Automatic via `deploy-pages.yml`. SPA fallback copies `index.html` to `404.html`.
- **Keio server**: Manual. Run `npm run build:keio`, download ZIP from GitHub Actions artifacts, upload to `public_html` via Cyberduck.
- **Keio fallbacks**: `scripts/generate-keio-fallbacks.mjs` creates server-side fallback files for client routes (needed because Keio server doesn't support SPA rewrites).

## okubo-personal-page (Secondary Project)

Uses **pnpm**, React 19, Tailwind CSS 4, wouter (not React Router), and has an Express backend (`server/`). Separate from the main portal — different package manager and stack versions.

```bash
cd okubo-personal-page
pnpm install
pnpm dev                  # Dev server
pnpm build                # Build client + server
pnpm check                # TypeScript check
```
