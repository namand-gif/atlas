# Atlas Lighting & Home — Dual-Brand Storefront (WizCommerce demo)

A single-file responsive prototype of the Atlas Lighting & Home storefront with an in-page brand switcher that flips header, footer, palette, content, and product set between **Atlas Lighting & Home** and **Thomas Lighting** — built per the customer's filled "Easy Website Design Brief" and the issue list in `Atlas & Thomas.xlsx`.

## How to open
Double-click `index.html`. No build step.

## Routes (hash-based)
- `#/` — Home
- `#/shop` — PLP (filters left, 5-col grid, pagination)
- `#/product` — PDP (gallery + variants + accordions + related + recently viewed)
- `#/login` — Trade sign-in / apply

## Brand switching
Header icon (account dropdown) → "Switch to ..." button. Only the alternate brand is shown. Atlas is gray/white; Thomas is navy with #366bab accents and a banner texture.

## Files
- `index.html` — full site (HTML + CSS + JS inline)
- `assets/atlas-logo.png` — Atlas wordmark (extracted from Atlas & Thomas.xlsx)
- `assets/thomas-logo.png` — Thomas wordmark (extracted)
- `assets/atlas-header.png`, `thomas-header.png` — header strips
- `assets/thomas-scrolling.png` — Thomas hero banner (used as Thomas hero background)
- `notes.md` — audit summary, decisions, assumptions
- `notes-tech.md` — engineering integration map
- `notes-product.md` — implementation team brief
- `notes-csm.md` — customer demo talking points

## Demo login
Click the account icon → "Sign in" link OR navigate to `#/login` and submit any email/password. The body class `user-logged-in` is toggled — pricing, MOQ, and Add-to-Cart become visible. Logged-out users see no price (no "Unlock Price" pill either, per the issue list).
