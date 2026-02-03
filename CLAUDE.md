# CLAUDE.md - Project Context

This file provides context about this project for Claude Code sessions.

## Project Overview

This is a personal HTML widgets collection designed to be embedded across note-taking applications. The widgets are built with Svelte and compiled to static HTML files hosted on GitHub Pages.

**Repository:** `gunt3001/widgets`
**Live URL:** `https://gunt3001.github.io/widgets/`

## Architecture

- **Framework:** SvelteKit with static adapter (`@sveltejs/adapter-static`)
- **Language:** TypeScript
- **Styling:** Tailwind CSS
- **Build Output:** Static HTML files in `build/` directory
- **Hosting:** GitHub Pages
- **Routing:** Each widget has its own URL route (e.g., `/relative-time`, `/seasons`)

## Current Widgets

### 1. Relative Time (`/relative-time`)
- **Purpose:** Display relative time between a specified time and current time
- **Examples:** "2 hours ago", "in 3 days", "just now"
- **Status:** Planned (port from existing widget)
- **Input:** Time parameter (likely via query string)
- **Output:** Formatted relative time string

### 2. Seasons (`/seasons`)
- **Purpose:** Show the week number of the current season
- **Seasons:** Winter, Spring, Summer, Fall
- **Status:** Planned (port from existing widget)
- **Input:** None (uses current date)
- **Output:** Current season and week number within that season

## Development Workflow

1. **Install dependencies:** `pnpm install`
2. **Start dev server:** `pnpm dev`
3. **Build for production:** `pnpm build`
4. **Preview build:** `pnpm preview`

## Deployment

The project uses static site generation. When changes are pushed to the repository, GitHub Actions should automatically build and deploy to GitHub Pages from the `build/` directory.

## Key Configuration Files

- `svelte.config.js`: SvelteKit configuration with static adapter
- `tailwind.config.js`: Tailwind CSS configuration
- `tsconfig.json`: TypeScript configuration
- `vite.config.ts`: Vite build configuration

## Design Principles

1. **Embeddable:** Widgets should work when embedded in iframes
2. **Lightweight:** Minimal dependencies, small bundle sizes
3. **Self-contained:** Each widget is independent
4. **Responsive:** Works across different screen sizes
5. **Accessible:** Follow web accessibility standards

## Important Notes

- This is a **personal project** - widgets are tailored for specific use cases
- Widgets are meant to be **embedded** in note-taking apps, so consider iframe constraints
- Each widget should have its **own route** in SvelteKit
- Static generation is **required** - no server-side rendering needed
- The project is a **port** of existing widgets, so reference any existing implementations if available

## Future Considerations

- Additional widgets can be added as separate routes
- Each widget should be documented in README.md with a live demo link
- Consider URL parameters for customization (colors, sizes, formats)
- Ensure widgets update dynamically (e.g., relative time should tick)

## Common Tasks

### Adding a New Widget

1. Create a new route in `src/routes/[widget-name]/+page.svelte`
2. Implement the widget component
3. Update README.md with description and live demo link
4. Test locally with `pnpm dev`
5. Build and verify with `pnpm build && pnpm preview`
6. Commit and push to deploy

### Testing Embeddability

Create an HTML file with an iframe pointing to the local dev server:
```html
<iframe src="http://localhost:5173/[widget-name]" width="300" height="200"></iframe>
```

## Questions to Ask User

When working on widgets, consider asking about:
- Preferred time format (12h/24h, timezone handling)
- Season definitions (meteorological vs astronomical)
- Color schemes and theming preferences
- Animation or transition preferences
- Error handling approaches
- Query parameter naming conventions
