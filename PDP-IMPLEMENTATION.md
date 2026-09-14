# Editorial product page

Implemented in the existing Tinker 4.1.5 theme. The development preview is theme `155887075496`; the live theme was not published.

## Architecture

- `templates/product.json`: existing default product template, configured for the editorial layout and native carousel.
- `sections/product-information.liquid`: existing product section and single Product JSON-LD; loads scoped presentation CSS and editor variables.
- `snippets/product-information-content.liquid`: original product component, media and details layout.
- `blocks/_product-media-gallery.liquid` and `snippets/product-media-gallery-content.liquid`: existing media carousel, thumbnails, zoom, deferred video and models. Added configurable badge, inactive heart, arrows and counter. The counter uses the existing slideshow `current` ref.
- `snippets/variant-main-picker.liquid`, `assets/variant-picker.js`, and `assets/variant-resolution.js`: original Shopify option resolution and variant section updates. Unavailable options are disabled in the editorial PDP.
- `snippets/price.liquid` and `assets/product-price.js`: original money formatting and variant price replacement. The translated percentage badge lives inside `priceContainer` so it updates with the price.
- `blocks/buy-buttons.liquid`, `blocks/quantity.liquid`, `assets/product-form.js`: unchanged real product form, quantity rules, gift-card behavior, accelerated checkout and cart submission.
- `assets/cart-drawer.js`, `assets/cart-icon.js`: unchanged drawer opening and count updates.
- `assets/product-editorial.css`: scoped PDP styling; desktop split at 990px, stacked tablet, mobile treatment below 768px. The existing header architecture and its native breakpoints remain intact.
- `blocks/product-editorial-intro.liquid`: escaped dynamic title/type and optional concise description. Full product description remains in its disclosure.
- `blocks/product-benefits.liquid`, `sections/product-editorial-story.liquid`: editable benefits, features, image pickers/captions and divider; shared small icon/item snippets.

## Theme Editor

Under Product information, enable Editorial layout and adjust title/price size, text, borders and button color. Background and information spacing reuse existing controls. The theme's existing Instrument Serif and Instrument Sans fonts are reused.

Under Product media, retain Carousel, thumbnails for both desktop and mobile, and Left thumbnail position for the reference composition. Adjust thumbnail width (now up to 100px), radius, gap, image ratio, zoom, arrows, counter and the product tag that enables the badge. The over-image counter is shown with thumbnail pagination; other pagination modes retain native controls without duplicate counter refs.

Product introduction controls description visibility and the 35-word synopsis. Product benefits contains four icon/title/description groups. Shipping thresholds and return periods can be expressed in those merchant-editable descriptions; no commercial promises were invented.

Product storytelling controls four features, four image pickers/captions, and divider text/spacing. The current default template's detail image selections come from the existing product photography. These are template settings, so use separate product templates or dynamic image sources when products need different storytelling photos/copy.

The heart is disabled and labeled “Wishlist unavailable”; it does not store favorites. Turn it off when adding an actual wishlist app.

## Verification completed

- Shopify Theme Check: zero errors; six warnings already present before the change (header settings count and unused divider doc parameters).
- Real Shopify product render: no Liquid errors; one PDP H1 and one Product JSON-LD object.
- All eight existing product variants: correct product form variant ID, selected size/color, 37% sale calculation and featured media for each color.
- Actual gallery render: ten media slides, ten keyboard-focusable thumbnails and dynamic `1 / 10` counter.
- Primary image: eager loading and high fetch priority. Four detail images: HTTP 200, responsive image URLs, lazy loading.
- Isolated cart API test: added quantity two of one variant and quantity one of another; verified two lines, count three, and returned cart-drawer section HTML. Removed those test lines and verified the isolated cart was empty.
- Cart, variant, slideshow and price JavaScript remain unchanged.

## Verification still required

Browser tools reported no available browser; the in-app browser was also unavailable. No browser screenshots, rendered-width measurements, console inspection, interactive swipe/zoom tests or drawer animation checks were possible. API verification does not establish that those client-side behaviors work.

Check the real preview at 320, 375, 390, 414, 430, 768, 1024, 1280, 1440 and 1920px for horizontal overflow, header/logo fit, thumbnail scrolling, sticky gallery behavior, title wrapping and four-column benefits. Compare screenshots with both supplied references.

Only one catalog product was available (ten images, eight available color/size variants, sale pricing). Products with zero/one media, video, external video, models, no options, sold-out options/products and no compare-at price still need runtime coverage. Their existing Liquid and JavaScript paths were retained, but this is not a substitute for testing those fixtures.

A full pre-change backup is stored beside the theme in `../pdp-backup-20260914-084218`.
