# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

**This is a template starter repository.** Update this file as you add features, change architecture, or establish new patterns.

## Build & Development Commands

```bash
bun run dev       # Start development server with hot reload
bun run build     # Production build
bun run start     # Start production server
bun run lint      # Check code with Biome
bun run format    # Format code with Biome
```

## Architecture

**Stack:** Next.js 16 (App Router) + TypeScript + Tailwind CSS v4 + Bun

**Directory Structure:**
- `src/app/` - Next.js App Router pages and layouts
- `src/components/ui/` - 60+ pre-generated shadcn/ui components
- `src/hooks/` - Custom React hooks
- `src/lib/utils.ts` - Utility functions including `cn()` for className merging

**Key Patterns:**
- Server Components by default (use "use client" sparingly)
- Class Variance Authority (CVA) for component variants
- `asChild` prop pattern for polymorphic components via Radix Slot
- Path alias: `@/*` maps to `src/*`

**Styling:**
- Tailwind CSS v4 with CSS variables (OKLch color space)
- Dark mode via `next-themes` (class-based toggle)
- Semantic color tokens: primary, secondary, accent, destructive, muted

**Forms:**
- `react-hook-form` + `zod` for validation
- Form components in `src/components/ui/form.tsx`

## Adding New UI Components

```bash
npx shadcn-ui@latest add [component]
```

Components are generated locally in `src/components/ui/`, not installed as npm packages.

## Code Quality

Uses Biome (not ESLint/Prettier) for linting and formatting. Configuration in `biome.json`.

## Project Management (Linear)

This project uses Linear for issue tracking via MCP integration.

**Workflow:**
1. Create a new Project in the "Projects" team for each app built from this template
2. Create issues within that project to track features, bugs, and tasks
3. Update issue status as work progresses

**Common Linear operations:**
- `mcp__linear-server__create_project` - Create a project in team "Projects"
- `mcp__linear-server__create_issue` - Create issues with `team: "Projects"` and `project: "<project-name>"`
- `mcp__linear-server__update_issue` - Update issue status, assignee, etc.
- `mcp__linear-server__list_issues` - List issues for a project
