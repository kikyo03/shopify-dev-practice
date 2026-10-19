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
