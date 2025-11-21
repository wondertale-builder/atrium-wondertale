# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project overview

- This `web/` package is a Next.js App Router frontend written in TypeScript.
- Runtime and tooling are Bun-first (note the `bun.lock` file); prefer `bun` for running scripts.
- Styling uses Tailwind CSS v4 via the new `@tailwindcss/postcss` plugin and `@theme` API (`src/app/globals.css`).
- The stack and long-term product scope are described in `guide.md`. The intended ecosystem includes:
  - Next.js + React
  - Clerk for authentication
  - tRPC for type-safe APIs
  - Drizzle ORM with Neon DB
  - Fastify as the backend HTTP server
  - shadcn/ui, Tailwind CSS, React Flow for UI
  - Resend for email, PostHog for analytics
- Many of these backend- and infra-related libraries are already installed in `package.json` but not yet wired into this `web/` app; expect additional backend or shared code to be added later in this repo or a sibling service.

## Commands

Use Bun as the default package manager in this directory.

- **Install dependencies**
  - `bun install`
- **Run the development server**
  - `bun dev`
  - Starts the Next.js dev server on `http://localhost:3000`.
- **Build for production**
  - `bun run build`
  - Runs `next build` using the config in `next.config.ts`.
- **Start the production server**
  - `bun run start`
  - Runs `next start` to serve the built app.
- **Lint the project**
  - `bun run lint`
  - Runs ESLint using `eslint.config.mjs` (Next.js core-web-vitals + TypeScript presets with customized ignores).

### Tests

- There is currently **no `test` script** in `package.json` and no test runner configured in this `web/` package.
- Before assuming a test command exists, inspect `package.json` and any future `tests/` or `__tests__/` directories. Once tests are added, update this section with:
  - The main test command (e.g. `bun test` or `bun run test`).
  - How to run a single test file or test name.

### Deployment (Sevalla CLI)

- Keep the Sevalla API key in an environment variable, not in source:
  - `SEVALLA_API_KEY={{SEVALLA_API_KEY}}`
- Example local deployment flow from this `web/` directory:
  - Ensure dependencies are installed: `bun install`
  - Build the app: `bun run build`
  - Deploy via Sevalla CLI (example): `sevalla deploy --api-key "$SEVALLA_API_KEY"`
- If the Sevalla CLI or project configuration changes, update these commands and document any required config files or flags.

## Code structure and conventions

### High-level layout

- **App entrypoints**
  - `src/app/layout.tsx`
    - Defines the `RootLayout` component for the App Router.
    - Uses Vercel's Geist and Geist Mono fonts (`next/font/google`) and applies them via CSS variables.
    - Imports global styles from `src/app/globals.css`.
  - `src/app/page.tsx`
    - Current home page with a simple marketing-style layout and links to Next.js/Vercel resources.
    - Uses Tailwind utility classes for layout, theming, and dark mode.
- **Styling**
  - `src/app/globals.css`
    - Imports Tailwind CSS via `@import "tailwindcss";`.
    - Defines CSS custom properties for `--background` and `--foreground` and maps them into Tailwind theme tokens using `@theme inline`.
    - Applies base `body` styles and ties in the Geist font CSS variables from `layout.tsx`.
- **Static assets**
  - `public/` contains static images such as `next.svg`, `vercel.svg`, `globe.svg`, etc., used by the starter page.

### TypeScript and module resolution

- `tsconfig.json` configures the TypeScript compiler with strict settings and Next.js plugin support.
- Path aliases:
  - `@/*` resolves to `./src/*`.
  - When adding new modules, prefer importing from `@/…` instead of relative `../../` chains.

### Configuration files

- `next.config.ts`
  - Currently uses the default `NextConfig` shape with a placeholder comment for future options.
  - When you modify framework-level behavior (image domains, experimental flags, redirects, etc.), do it here.
- `eslint.config.mjs`
  - Uses `eslint-config-next` (`core-web-vitals` and `typescript` variants) via `defineConfig`.
  - Overrides the default ignores with `globalIgnores` to explicitly ignore `.next/**`, `out/**`, `build/**`, and `next-env.d.ts`.
- `postcss.config.mjs`
  - Configures PostCSS to use `@tailwindcss/postcss`; keep Tailwind-related plugins wired through this file.

### Product and stack guide

- `guide.md` contains the detailed product breakdown and technology stack for Atrium CRM.
  - Treat it as the source of truth for planned major features (data model, workflows, AI assistants, integrations, collaboration, platform features, non-functional requirements).
  - When adding new domains (e.g., workflows, AI, integrations), cross-check your design against the corresponding section in `guide.md` to stay aligned with the overall plan.

## How to extend the app

- New pages and routes should be added under `src/app/` using the Next.js App Router conventions.
- Shared UI components, hooks, and utilities should live under `src/` (e.g., `src/components`, `src/lib`) and be imported via the `@/` alias.
- As backend APIs (tRPC, Fastify, Drizzle/Neon) are introduced into this repo, document their directory layout and key routers/schemas here so future agents can quickly locate the source of truth for business logic.
