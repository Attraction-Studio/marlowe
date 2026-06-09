# Astro Starter Kit: Minimal

## Prototype Versions

- `/` - version log with links to each prototype.
- `/staggered-reveal/` - DOM tile reveal from top-left to bottom-right.
- `/image-set-hover/` - original 4x5 prepared-image hover grid using CSS backgrounds.
- `/image-set-flex/` - 4x5 prepared-image hover grid using flex rows and natural image height.
- `/image-set-flex-two/` - flex-row image grid limited to the first two prepared image sets.
- `/image-set-flex-two-once/` - two-frame flex-row image grid where each tile can reveal only once.
- `/image-set-flex-locked/` - flex-row image grid with one-at-a-time reveals and round-based frame progression.

```sh
npm create astro@latest -- --template minimal
```

> 🧑‍🚀 **Seasoned astronaut?** Delete this file. Have fun!

## 🚀 Project Structure

Inside of your Astro project, you'll see the following folders and files:

```text
/
├── public/
├── src/
│   └── pages/
│       └── index.astro
└── package.json
```

Astro looks for `.astro` or `.md` files in the `src/pages/` directory. Each page is exposed as a route based on its file name.

There's nothing special about `src/components/`, but that's where we like to put any Astro/React/Vue/Svelte/Preact components.

Any static assets, like images, can be placed in the `public/` directory.

## 🧞 Commands

All commands are run from the root of the project, from a terminal:

| Command                   | Action                                           |
| :------------------------ | :----------------------------------------------- |
| `npm install`             | Installs dependencies                            |
| `npm run dev`             | Starts local dev server at `localhost:4321`      |
| `npm run build`           | Build your production site to `./dist/`          |
| `npm run preview`         | Preview your build locally, before deploying     |
| `npm run astro ...`       | Run CLI commands like `astro add`, `astro check` |
| `npm run astro -- --help` | Get help using the Astro CLI                     |

## 👀 Want to learn more?

Feel free to check [our documentation](https://docs.astro.build) or jump into our [Discord server](https://astro.build/chat).
