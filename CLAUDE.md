# Kamui storefront

Shopify theme for Kamui, built on Shopify's Skeleton theme. `config/settings_schema.json` still reports Skeleton 0.1.0.

## Commands

- Preview: `shopify theme dev --store <store>.myshopify.com`
- Lint: `shopify theme check`. Keep it at zero offenses before committing Liquid changes.

## What is custom so far

- `sections/header.liquid`: announcement bar, centered logo, icon row, and the menu drawer.
- `sections/hero.liquid`: full-height image, heading, and email signup. It is the only section on the homepage (`templates/index.json`).
- `assets/`: `logo-kamui.svg`, the `icon-*.svg` set, and the default hero images.
- Everything else, including `README.md`, is still stock Skeleton.

## Conventions

- Brand tokens (`--color-brand: #9f100c`, `--header-height`, `--announcement-height`) are defined in the `{% stylesheet %}` of `sections/header.liquid`. Reuse them instead of hardcoding values.
- Inline SVGs with `{{ 'name.svg' | inline_asset_content }}` so they inherit `currentcolor`.
- Prefer platform features over JavaScript. The menu drawer is a native `popover`.
- Keep locale strings in sentence case and apply uppercase in CSS, as `.hero__heading` does.
- A `ponytail:` comment marks a deliberate shortcut and names when to upgrade it.

## Gotchas

- The header and hero are coupled. The hero pulls itself up by `--header-height` to sit under the header, and `body:has(.hero) .header` switches the header to white text. Check both when changing either.
- The hero uses `hero-desktop.webp` and `hero-mobile.webp` from `assets/` until a merchant picks images in the theme editor.
- The hero signup is a `customer` form tagged `newsletter,early-access`. Keep those tags unless the marketing segments change.
- The theme editor can overwrite `templates/*.json`, section group JSON, and `config/settings_data.json`. Run `shopify theme pull` before editing them if the live theme has been customized.
- `copilot-instructions.md` is a copy of `AGENTS.md`. Update them together.

## Agent tooling

- OpenSpec: plan non-trivial changes with `/opsx:propose`, build them with `/opsx:apply`, and finish with `/opsx:archive`. Specs live in `openspec/`. Refresh the generated files with `openspec update`.
- Ponytail and Karpathy guidelines: skills in `.claude/skills/`. Ponytail is also enabled as a plugin in `.claude/settings.json` because its always-on mode needs the plugin's hooks. Accept the install prompt when opening the repo.

## Shopify platform rules

@AGENTS.md
