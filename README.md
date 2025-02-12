# SvelteClick

SvelteClick is an idle clicker game implemented in Svelte. It is intended to be
quite difficult and encourage user interaction. Planned features:

- Button moves around the page on each click.
- Button is difficult to distinguish from achievements.
- Button uses randomized classes and coexists with hidden buttons to make
  script automation difficult.

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://svelte.dev/docs/kit/adapters) for your target environment.
