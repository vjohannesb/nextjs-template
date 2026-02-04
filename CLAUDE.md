# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Initialization (READ THIS FIRST)

**If the README title is "Next.js Template", this repo needs initialization.**

When the user describes what they want to build:

1. **Create a project name** - Short, memorable, kebab-case (e.g., "gym-tracker", "recipe-vault")
2. **Update these files immediately:**
   - `README.md` - Change title and description to match the project
   - `package.json` - Update the `name` field
   - `src/app/layout.tsx` - Update metadata `title` and `description`
3. **Create Linear project** - Use `mcp__linear-server__create_project` with:
   - `name`: The project name (title case, e.g., "Gym Tracker")
   - `team`: "Projects"
   - `description`: Brief description of what we're building
4. **Create initial Linear issues** - Use `mcp__linear-server__create_issue` for each:
   - Assign to `"me"`
   - Set appropriate `priority` (1=Urgent, 2=High, 3=Normal, 4=Low)
   - Add to the project you just created
   - Apply relevant labels (see Linear Integration section)
   - Break down the user's request into actionable issues
5. **Update this CLAUDE.md** - Add a "Project Status" section below with:
   - What the project is
   - Key decisions made
   - Current state

6. **Commit the initialization** - Single commit with all the setup changes

Then proceed to plan and build. Be proactive—make reasonable assumptions and move fast. Only ask questions for critical decisions that significantly impact architecture.

---

## Project Status

*Not yet initialized. Awaiting project description.*

---

## Build & Development Commands

```bash
bun run dev       # Start development server with hot reload
bun run build     # Production build
bun run start     # Start production server
bun run lint      # Check code with Biome
bun run lint:fix  # Check and auto-fix with Biome
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

## Linear Integration

**Team:** Projects
**Workflow:** Each project gets its own Linear Project with issues tracking features, bugs, and tasks.

**Labels** (use when creating issues):
- `feature` - New functionality
- `improvement` - Enhancing existing functionality
- `bug` - Something broken
- `ui` - Frontend and design work
- `infrastructure` - Build, deploy, config
- `integration` - External services, APIs
- `tech debt` - Refactoring, cleanup
- `future` - Ideas for later, not now
- `agent` - AI/agent related
- `adapter` - Adapter implementations

**During development:**
- Update issue status to "In Progress" when starting work
- Mark issues "Done" when complete
- Create new issues as scope expands or new tasks emerge
- Keep issues granular and actionable

Common operations:
- `mcp__linear-server__list_issues` - Check current issues (use `project` filter)
- `mcp__linear-server__update_issue` - Update status as work completes
- `mcp__linear-server__create_issue` - Add new issues as scope expands

## Development Flow

After completing work, follow this flow:

1. **Run tests** (if available): `bun test`
2. **Lint and fix**: `bun run lint:fix`
3. **Commit** with conventional commit message:
   ```
   type(scope): description

   [optional body]
   ```
   Types: `feat`, `fix`, `chore`, `docs`, `style`, `refactor`, `test`, `perf`
4. **Push** to remote
