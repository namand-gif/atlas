# Atlas & Thomas — Product / implementation notes

## Business architecture preserved
- **Two brands under one storefront.** Atlas Lighting & Home is the parent; Thomas Lighting is a sub-brand distributed via Atlas. The brand switcher (per customer brief, modeled on Sagebrook + Elevarre) keeps each brand visually distinct without splitting the catalog management story.
- **Trade-only commerce.** Pricing, MOQ, and case-pack are visible only after sign-in. Sign-up is a "request account" flow — not a self-serve checkout — and assumes manual approval (~1 business day).
- **Net-30 terms.** Surfaced in the announcement bar and footer copy.
- **No public consumer pricing.** Per issue 25, logged-out users see no price at all and no "Unlock Price" CTA. The card simply omits the price row.

## Brand-specific differences (configuration the customer asked for)
| Setting | Atlas | Thomas |
|---|---|---|
| Logo size in header | 52 px | 72 px (issue 8) |
| Primary palette | gray + white (issue 1) | navy + #366bab blue (issue 2) |
| Hero background | CSS gradient (no banner supplied) | `assets/thomas-scrolling.png` (issue 3) |
| First nav item | Lighting | Lighting by Collection (issue 21) |
| Wishlist in header | Yes | Yes — explicitly requested (issue 11) |
| Featured Collections count | 6 (issue 17) | 6 |
| Featured Products count | 4 desktop / 2 mobile | 4 desktop / 2 mobile (issue 16) |
| Footer "Opportunity Buys" link | Yes (issue 19) | Yes |

Same on both: fonts (Cormorant + Inter), header background `#f6f6f6`, feature band `#dddddd`, body type 16 px, button height 52 px.

## Category tree (preserved verbatim from live site)
- **Lighting**
  - Indoor: Chandelier, Floor Lamp, Flush Mount, Lighting Part - Component, Mini Pendant, Pendant, Recessed, Sconce, Semi Flush Mount, Table Lamp, Vanity Light
  - Outdoor: Outdoor Flush Mount, Outdoor Pendant, Outdoor Wall Sconce, Post Light, Outdoor Table Lamp
- **Decor**
  - Decorative Accessory: Bowl - Tray, Box - Bin - Basket, Candle - Candleholder, Easel, Ornamental Accessory, Planter, Pouf, Vase - Jar - Bottle, Clock
  - Wall Decor: Clock, Mirror, Wall Art, Wall Shelving
- **Furniture**
  - Seating: Bench - Ottoman, Chair, Stool, Sofa
  - Storage: Bookcase - Shelf, Cabinet - Credenza, Chest, Media - Entertainment
  - Table: Accent Table, Coffee Table, Console Table - Desk, Dining Table, Bar Cart
  - Outdoor Furniture: Outdoor Table
- **Thomas Lighting** — links to the Thomas brand context (header/footer flip)

## Merchandising flows
- **PLP filter logic.** Sidebar groups: Category, Finish, Material, Width. Multi-select. Counts shown next to each option. Sort options: Recommended, New arrivals, Bestsellers, Name A–Z.
- **Product card data shown.** SKU, Name (3-line clamp — issue 23), Finish + Material concatenation (issue 24), Price (logged-in only — issue 25), Case pack, Wishlist toggle, Quick view (hover-and-tap), Add-to-cart or Sign-in CTA.
- **PDP data shown.** Breadcrumbs, SKU, Spec sheet download, Category eyebrow, Product title, Short description block (issue 26 — visually elevated), MOQ + case-pack, Price (logged-in only) + small description note after price (issue 26), Finish variants (4 swatches), Add to cart, Add to wishlist, 4 accordions (Product details / Specifications / Shipping & lead time / Care & warranty), Related products rail (5-up), Recently viewed rail (5-up).
- **Cart badge.** Increments on add. Hidden when count is zero AND user is logged out.

## Login-gating rules
- **Logged out:** no prices anywhere; no MOQ on PDP; no Add-to-Cart button on card or PDP (CTA is "Sign in to buy"); cart icon visible but badge hidden.
- **Logged in:** prices visible; MOQ visible; Add-to-Cart enabled; cart badge updates on add.

There is **no intermediate "preview" state** — the customer's brief explicitly rejected the "Unlock Price" pill pattern. Logged-out users see a clean card with no pricing surface at all.

## Migration data needed from customer
| Item | Status | Owner |
|---|---|---|
| Final Atlas wordmark (live vs XLSX divergence noted on Assets sheet) | Confirm | Customer |
| Real product catalog feed (SKU + name + finish + material + MOQ + case pack + image URL + category) | Provide | Customer |
| Thomas product catalog (separate brand feed) | Provide | Customer |
| Trade-show booth assignments + dates for 2026 | Provide | Customer |
| Real hero photography (currently CSS gradient on Atlas) | Provide | Customer |
| Showroom photography for 6 collection tiles per brand | Provide | Customer |
| Designer trade program copy block | Provide | Customer |
| Catalog PDFs for download | Provide | Customer |

## Channel / visibility
- **Web only** in this build. App is out of scope.
- **Default brand on home** is Atlas. Customer can flip the default by changing the `localStorage` fallback in the bootstrap.
- **Thomas brand** is reachable via the brand switcher (account dropdown), the "Thomas Lighting" nav link on Atlas, and the "Atlas Lighting & Home" link from the Thomas nav (reciprocal).
- **Opportunity Buys** link is in the Atlas footer Products column (issue 19). Confirm the destination URL — currently routes to `#/shop?cat=opportunity` placeholder.

## Known business-side gaps (raise with customer)
1. Net-30 terms enforcement is UI-only in the demo — the live platform needs to check the buyer's tier before allowing terms on checkout.
2. No real "request account" form submission yet — currently a tab in the login view.
3. No designer trade program landing page — footer link goes to `#` for now.
4. No dealer locator page — footer link goes to `#` for now.
5. No catalogs / showroom locations pages — footer links go to `#`.
6. Wishlist persistence (logged-in vs guest) needs a backend hook.
