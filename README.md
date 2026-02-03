# Personal HTML Widgets

A collection of personal HTML widgets built with Svelte and compiled to static HTML for embedding across note-taking applications. Each widget is accessible via its own URL route and hosted on GitHub Pages.

## Widgets

### Relative Time
Displays the relative time between a specified time and the current time (e.g., "2 hours ago", "in 3 days").

**Live Demo:** [https://gunt3001.github.io/widgets/relative-time](https://gunt3001.github.io/widgets/relative-time)

### Seasons
Shows the week number of the current season of the year (Winter, Spring, Summer, Fall).

**Live Demo:** [https://gunt3001.github.io/widgets/seasons](https://gunt3001.github.io/widgets/seasons)

## Development

Install dependencies:

```sh
pnpm install
```

Start the development server:

```sh
pnpm dev
```

## Building

To create a production build:

```sh
pnpm build
```

The static files will be generated in the `build` directory.

Preview the production build:

```sh
pnpm preview
```

## Deployment

This project is configured for static site generation and is deployed to GitHub Pages. The built files are served from the `build` directory.

To deploy:
1. Build the project: `pnpm build`
2. Push changes to the repository
3. GitHub Actions will automatically deploy to GitHub Pages

## Technology Stack

- **Svelte**: Component framework
- **SvelteKit**: Build tool with static adapter
- **TypeScript**: Type safety
- **Tailwind CSS**: Styling
- **GitHub Pages**: Hosting

## License

Personal project - all rights reserved.
