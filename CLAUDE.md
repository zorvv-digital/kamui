# Kamui storefront

Shopify theme for Kamui, built on Shopify's Skeleton theme. `config/settings_schema.json` still reports Skeleton 0.1.0.

## Commands

- Preview: `shopify theme dev --store kamui-rvf1gcfh.myshopify.com`
- Shared preview: the unpublished "Kamui preview" theme (#160426590430). Update it with `shopify theme push --store kamui-rvf1gcfh.myshopify.com --theme 160426590430`. The live theme is still Horizon.
- Lint: `shopify theme check`. Keep it at zero offenses before committing Liquid changes.

## What is custom so far

Git `main` is the source of truth. Make changes there and push them to themes from it, not in a theme first.

- Homepage (`templates/index.json`): `hero`, `featured-products`, `subscribe`, `collection-tiles`, `pattern`, `journey`.
- `sections/header.liquid`: optional announcement ticker (currently no announcements), centered logo, icon row (search, menu, account, cart), predictive search, and the menu drawer.
- `sections/hero.liquid`: full-height image with the heading, subheading, and early access button at bottom left.
- `sections/pattern.liquid`: placeholder until the pattern is confirmed. `sections/puzzle.liquid` is built but not on the homepage.
- `sections/subscribe.liquid`: the early access email signup.
- `sections/footer.liquid`: logo, social, policies, and about columns, copyright and payment icons, and a full-width wordmark on the bottom edge. The page slides up off it on scroll.
- `sections/main-*.liquid`: the product, collection, cart, search, blog, and other page templates.
- `README.md` is still stock Skeleton.

## Conventions

- Brand tokens (`--color-brand: #9f100c`, `--header-height`, `--announcement-height`) are defined in the `{% stylesheet %}` of `sections/header.liquid`. Spacing, type, and motion tokens (`--space-*`, `--text-*`, `--ease-out`) are in `assets/critical.css`. Reuse them instead of hardcoding values.
- Inline SVGs with `{{ 'name.svg' | inline_asset_content }}` so they inherit `currentcolor`.
- Prefer platform features over JavaScript. The menu drawer is a native `popover`.
- Keep locale strings in sentence case and apply uppercase in CSS, as `.hero__heading` does.
- A `ponytail:` comment marks a deliberate shortcut and names when to upgrade it.

## Gotchas

- The header and hero are coupled. The hero pulls itself up by `--header-height` to sit under the header, and `body:has(.hero) .header` switches the header to white text. Check both when changing either.
- The hero uses `hero-desktop.webp` and `hero-mobile.webp` from `assets/` until a merchant picks images in the theme editor.
- The hero's early access button links to `#subscribe`. That signup is a `customer` form tagged `newsletter,early-access`. Keep those tags unless the marketing segments change.
- The footer reveal in `sections/footer.liquid` gives `main` a background and stacks the header group above it. Content that should cover the footer has to live inside `main`.
- `featured-products` shows the hand-picked `products` list in order when it is set, otherwise the collection.
- The theme editor can overwrite `templates/*.json`, section group JSON, and `config/settings_data.json`. Run `shopify theme pull` before editing them if the live theme has been customized.
- `copilot-instructions.md` is a copy of `AGENTS.md`. Update them together.

## Agent tooling

- OpenSpec: plan non-trivial changes with `/opsx:propose`, build them with `/opsx:apply`, and finish with `/opsx:archive`. Specs live in `openspec/`. Refresh the generated files with `openspec update`.
- Ponytail and Karpathy guidelines: skills in `.claude/skills/`. Ponytail is also enabled as a plugin in `.claude/settings.json` because its always-on mode needs the plugin's hooks. Accept the install prompt when opening the repo.

## Shopify platform rules

@AGENTS.md
