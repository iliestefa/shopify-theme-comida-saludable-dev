# Shopify Theme — Development Rules

## Stack
Shopify Liquid · Tailwind CSS v4 · Alpine.js v3 · Swiper v11 · Vite v5

## Images
- Always `{%- render 'image', image: object, ... -%}` — never `image_url` + `image_tag` directly
- Static asset fallback: `<img src="{{ 'file.png' | asset_url }}" width="" height="" loading="lazy" alt="">`
- Never `placeholder_svg_tag`

## Icons
- Always `{%- render 'icon', icon: 'name' -%}` — never inline SVG in sections
- Available icons: `account` `arrow` `caret` `chevron-down` `cart` `cart-empty` `close` `close-small` `discount` `error` `filter` `hamburger` `info` `minus` `pause` `play` `plus` `remove` `search` `share` `star` `success` `zoom` `facebook` `instagram` `twitter` `tiktok` `youtube` `pinterest`
- To add a new icon: add `{%- when 'name' -%}` in `snippets/icon.liquid`

## Alpine.js
- Header, footer, cart, PDP, PLP → register in `external/src/main.js`
- Secondary sections → inline with `{ once: true }` and `section.id` in the component name:
  ```liquid
  <div x-data="myComp_{{ section.id }}"></div>
  <script>
    document.addEventListener('alpine:init', () => {
      Alpine.data('myComp_{{ section.id }}', () => ({ open: false }))
    }, { once: true })
  </script>
  ```
- Cart store: `$store.cart`

## Swiper
- Use `window.Swiper` with Alpine `$refs` for container and pagination

## Tailwind v4
- No `tailwind.config.js` — tokens defined in `@theme {}` inside `external/src/main.css`
- Classes must always be complete — never concatenate dynamic strings
- Dynamic Liquid-generated classes → add via `@source` or `@utility` in `main.css`
- Custom classes used with `@apply` from another file → declare them as `@utility`
- `-down` breakpoints → already defined with `@custom-variant` in `main.css`
- Containers: `.c-container` and `.c-container.wide`

## Liquid
- Variables in `snake_case` — never prefix with `_`
- Schema `url` fields without `"default": ""`
- `<script defer>` — never use the `script_tag` filter
- Every direct `<img>` requires `width`, `height`, `loading`, `alt`

## Git
- Every new feature → create a `feature/feature-name` branch before starting
- Never work directly on `main`

## shopify theme check
Must return **0 offenses** before every commit.
