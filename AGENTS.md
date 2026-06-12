# AGENTS.md

## Project

SMBX World community homepage. Astro 6.x static site, Chinese (zh-CN), retro Mario-themed design.

## Commands

- `bun run dev` — start dev server (listens on 0.0.0.0)
- `bun run build` — production build to `dist/`
- `bun run preview` — preview production build
- `bun run deploy` — server deploy (runs `deploy.sh`: git pull → bun install → bun run build → rsync to `/data/wwwroot/www.smbx.world/`)

**Package manager: Bun.** Do not use npm/yarn/pnpm.

## Structure

```
src/
  pages/          # Route files (*.astro) — one file per page
  layouts/        # BaseLayout.astro (single layout, wraps all pages)
  components/     # BlockBox.astro (table-based colored box, main layout primitive)
  styles/         # global.css (single file, ~1400 lines, includes normalize.css)
public/
  images/         # Static assets (affiliates/, assets/, screenshots/, uploads/)
```

## Conventions

- **No lint, typecheck, or test commands configured.** TypeScript is Astro-strict only.
- All content is in Chinese. Maintain Chinese for any user-facing text.
- Layout uses `<table>` elements intentionally (retro design), not modern CSS grid/flex for main structure.
- `BlockBox` component accepts `color` prop: `blue | green | orange | white`. Each color has distinct sprite styling.
- `BaseLayout` accepts optional `theme` prop: `default | desert | ice`. Themes swap background/pipe/footer images.
- Pages with data (episodes, links) define content arrays in the frontmatter section.
- Lightbox for images is implemented inline in `BaseLayout.astro` (vanilla JS, no library).
- `BlockBox` has client-side height adjustment script to align content to 32px grid.

## Deploy

`deploy.sh` runs on the server (not locally). It pulls `main`, builds, and rsyncs `dist/` to the web root. The script assumes Bun is at `$HOME/.bun/bin`.
