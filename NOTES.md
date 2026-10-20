# Dawn Theme Notes

## How a product page gets built

1. Request comes in for a product page
2. `layout/theme.liquid` is the outer shell, and `{{ content_for_layout }}` is where the page content goes
3. `templates/product.json` lists which sections the page uses and their order
4. `sections/main-product.liquid` builds the product info (title, price, variants, buy button)
5. Snippets (in `snippets/`) are small reusable pieces pulled in with `{% render %}`

## Things I learned

- `{% comment %}` is a Liquid comment and never reaches the browser. `<!-- -->` is an HTML comment and does.
- when changing something it affects everything so be careful
-

## Edits I made

- Added "(test)" next to the product title in `main-product.liquid`
- Added an HTML comment in `theme.liquid`
- Changed the header background in `header.liquid`

## Liquid basics

- `{{ }}` prints a value, `{% %}` runs logic, and `|` applies a filter
- `{% for product in collections.all.products limit: 6 %}` loops through products. `forloop.index` is the current number.
- `{% if %}` shows something only when a condition is true
- `{% assign %}` stores a value in a variable
- `money` turns a raw price (50000) into a formatted one (₱500.00). Prices are stored in the smallest unit.
- `{% comment %}` is a Liquid comment and never reaches the browser. `<!-- -->` is an HTML comment and does.

### Percent-off recipe

{%- assign saved = product.compare_at_price | minus: product.price -%}
{%- assign percent = saved | times: 100.0 | divided_by: product.compare_at_price | round -%}

- Use `100.0` so the division keeps decimals
- Do the math on raw numbers first, then use `money` only when printing

### Dawn sale badge

- Edited `snippets/card-product.liquid` to show "Sale -X%"
- The card has **two** badge blocks (`Badge-...` and `NoMediaStandardBadge-...`). Edit both or some cards won't change.
- In the card snippet the variable is `card_product`, not `product`. Other themes may use different names.
- A section added in the theme editor doesn't stay until I click **Save**

## First custom section

- Built `sections/promo-banner.liquid` with a `{% schema %}`
- Schema settings (text, url, color) are what show up in the theme editor sidebar
- `section.settings.<id>` reads a setting's value in the Liquid
- `presets` in the schema is what makes the section appear in "Add section"
- Sections have schema settings, snippets don't. Snippets get data through `{% render %}`.
- `{% stylesheet %}` holds the section's CSS. Colors from settings use a small inline style since the value changes per section.

## Workflow

1. Write structure in VS Code (sections, Liquid, CSS, schema)
2. Change content and options in the theme editor, then click **Save**
3. Before stopping, run `shopify theme pull` so editor changes land in my local files
4. Commit and push

# Shopify Theme Practice (Dawn)

A practice project where I learn Shopify theme development by customizing Dawn, Shopify's reference theme. I'm using it to build my Liquid, section, and theme workflow skills.

## What I built

- **Percent-off sale badge:** customized Dawn's product card (`snippets/card-product.liquid`) so sale items show "Sale -X%" instead of just "Sale"
- **Promo banner section:** a custom section with editable heading, subtext, button, and colors
- **Hero carousel section:** a fade carousel built with blocks, with editor settings for:
  - Slides (image, heading, subtext, button)
  - Banner height, autoplay, speed, and fade duration
  - Fonts, sizes, and alignment
  - Separate heading, subtext, and overlay colors
  - Button style (solid or outline) and shape

## Tech

- Shopify CLI
- Liquid
- HTML, CSS, and vanilla JavaScript
- Dawn theme (Online Store 2.0)

## Run it locally

1. Install Node.js and the Shopify CLI: `npm install -g @shopify/cli@latest`
2. Clone this repo and `cd` into it
3. Run: `shopify theme dev --store [your-store].myshopify.com`
4. Open the preview link it prints

## What I learned

- How a Shopify theme is put together (layout, templates, sections, snippets)
- Liquid objects, tags, and filters
- Schema settings and blocks for editor-friendly sections
- Building a fade carousel with CSS transitions and a little JavaScript
- Working with the CLI and the theme editor together

## Screenshots

## Live demo
