# Atlas & Thomas — Engineering integration notes

## File map
```
site/
├── index.html      single self-contained file (HTML + CSS + JS)
├── assets/
│   ├── atlas-logo.png        571 × 366
│   ├── thomas-logo.png       975 × 550   (rendered 72px tall in header — bigger than Atlas per issue 8)
│   ├── atlas-header.png      1877 × 259  (optional header strip)
│   ├── thomas-header.png     1883 × 236  (optional header strip)
│   └── thomas-scrolling.png  1440 × 960  (Thomas hero background — issue 3)
├── README.md
├── notes.md
├── notes-tech.md
├── notes-product.md
└── notes-csm.md
```

## Architecture
- **Single HTML file.** Inline `<style>`, inline `<script>`. No frameworks, no build, no npm. Page runs offline by double-clicking.
- **Brand switching via `body[data-brand]`** — single source of truth. All brand-aware CSS is keyed on this attribute. JS function `applyBrand(name)` re-renders nav, collections, featured products, story, trade-show grid, and rails when the brand flips. Selection is persisted to `localStorage` (`atlas-thomas-brand`).
- **Hash routing** — `route()` listens on `hashchange` and toggles `.view.active`. Routes: `#/`, `#/shop`, `#/product`, `#/login`. No external router; ~10 LOC.

## CSS token reference (`:root` plus brand overrides)
| Token | Atlas | Thomas | Source |
|---|---|---|---|
| `--brand-primary` | `#1f2226` | `#1e3a5f` | inferred from audit + customer brief |
| `--brand-accent` | `#2b2e33` | `#366bab` | customer-supplied (template field 5) |
| `--brand-cta` | `#1f2226` | `#366bab` | customer-supplied |
| `--surface-header` | `#f6f6f6` | `#f6f6f6` | customer-supplied |
| `--surface-feature` | `#dddddd` | `#dddddd` | customer-supplied |
| `--text-strong` | `#1f2226` | `#1f2530` | derived for AAA contrast |
| `--btn-h` (primary) | 52 px | 52 px | older-B2B guardrail |
| `--fs-base` | 16 px | 16 px | older-B2B guardrail |

## Component → selector map
| Component | Selector | Notes |
|---|---|---|
| Announcement bar | `.announce` | Sticky top, brand-primary color |
| Sticky header | `header.site-header` | sticky at `top: var(--announce-h)` |
| Mobile drawer | `.drawer`, `.drawer-scrim` | controlled by `#openDrawer` + `#closeDrawer` |
| Hero | `.hero`, `.hero__media`, `.hero__copy` | copy at bottom (issue 9), media is absolute pseudo-element |
| Featured collections | `.fc-grid`, `.fc-card` | 6-tile, responsive 6→3→2 |
| Category collage | `.collage`, `.collage__left`, `.collage__right` | 1.2fr / 1fr — Lighting left, Furniture+Decor stacked right (issue 18) |
| Featured products | `.fp-grid`, `.pcard` | 4 / 3 / 2 cols (issue 16) |
| PLP filter sidebar | `.filters`, `.filters__group` | sticky-top, left of grid (issue 22) |
| PLP grid | `.plp-grid` | 5 / 4 / 3 / 2 cols (template field 9) |
| Product card | `.pcard` | login-gated price, finish+material row (issues 24, 25) |
| PDP | `.pdp__layout`, `.pdp__gallery`, `.pdp__short`, `.pdp__priceblock` | description above price block (issue 26) |
| Related / Recently Viewed | `.rail`, `.rail-grid` | 5-up grid, also shown at end of PLP |

## JS function reference
| Function | Responsibility |
|---|---|
| `applyBrand(name)` | Flip data-brand, swap logos, regenerate nav + collections + featured + shows + rails |
| `route()` | Hash-router; toggles `.view.active` |
| `pcardHTML(p)` | Returns the product card markup |
| `renderPlpGrid(B)` | Combines `features` + procedural filler → 20 cards on PLP |
| `renderRails(B)` | Populates Recently Viewed + Related rails |
| `setupHeader()` | Account dropdown open/close + brand-switch action + drawer open/close |
| `setupPdp()` | Accordion toggle + variant active state + gallery thumb active |
| `setupFilters()` | Filter group collapse + cart badge increment |
| `setupTabs()` | Sign-in / Apply tab switch |
| `setLogged(v)` | Toggle `body.user-logged-in` — CSS reveals price / MOQ |

## Login-gating model
```css
body:not(.user-logged-in) .pcard__price-amount { display: none; }
body:not(.user-logged-in) .pdp__price-amt    { display: none; }
body:not(.user-logged-in) .pdp__moq          { display: none; }
body.user-logged-in .pdp__login-note         { display: none; }
body:not(.user-logged-in) .pcard__btn-add    { display: none; }
body.user-logged-in       .pcard__btn-login  { display: none; }
```

Per issue 25, there is **no "Unlock Price" or "Login to See Price" pill in the DOM at all** — the logged-out price area is simply empty (CSS hides the price; no replacement label is rendered).

## Sticky offset stack
| Element | `top` | Computed offset |
|---|---|---|
| `.announce` | `0` | top of viewport |
| `header.site-header` | `var(--announce-h)` (36 px) | below announce |
| `.filters` (PLP) | `calc(var(--header-h) + var(--announce-h) + 20px)` | below header |

The header is **not** wrapped in a slot container, so the `display: contents` workaround isn't required, but it's worth flagging in case a CMS injects a wrapper.

## Responsive breakpoints
| Breakpoint | Behavior |
|---|---|
| `≥1280` | PLP grid 5-col, FC grid 6-col, header full |
| `1100–1280` | PLP grid 4-col, FC grid 3-col |
| `900–1100` | Search pill narrows, FC grid 3-col |
| `760–900` | Hamburger appears, main nav hides, search pill hides |
| `600–760` | FP grid 2-col, hero shorter |
| `<600` | FC grid 2-col, footer 1-col, newsletter form stacks |

## CMS / data integration hooks
Replace the JS arrays with API responses:
- `BRANDS.<brand>.collections` ← `/api/featured-collections?brand=`
- `BRANDS.<brand>.features` ← `/api/products?featured=true&brand=`
- `BRANDS.<brand>.shows` ← `/api/trade-shows?brand=`
- `renderPlpGrid(B)` should call `/api/products?cat=<from URL>&page=<n>` (50 per page)
- `pcardHTML(p)` already consumes `{ sku, name, finish, price, case, grad }` — map this to your product schema

The brand switcher only mutates the in-page DOM. For real navigation, you may want to route `?brand=thomas` queries through the backend so direct URLs land on the right brand.

## Known risks / cross-cutting concerns
1. **Logo asset divergence** — the Atlas logo in the XLSX differs from the one rendered on the live site. Pick one and replace.
2. **Hero gradient fallback** — Atlas hero uses a CSS gradient (no banner image supplied for Atlas); replace with a real photograph when available.
3. **Brand switcher persistence** — uses `localStorage`; if you switch to URL-driven brand selection later, drop the localStorage line.
4. **No analytics hooks wired** — add `data-analytics` attributes or fire `dataLayer.push` from `applyBrand()`, `pcard__btn-add`, `doLogin`.
5. **Trade-partner gating modal not included** — the existing platform may show a 1-per-session modal asking visitors to identify as a designer / dealer / retailer. Add via a single `localStorage` flag if needed.
6. **No real product API yet** — filler is procedurally generated to demo the grid; cut over before going live.
