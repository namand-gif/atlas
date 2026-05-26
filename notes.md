# Atlas & Thomas — Audit notes, decisions, and assumptions

## Sources used
1. **Easy Website Design Brief** (uploaded `.docx`) — brand, references, palette overrides, layout choices.
2. **Atlas & Thomas.xlsx** — 26-item issue list with Jira ticket links + Assets sheet (Thomas logo, Thomas scrolling banner, Atlas logo, Thomas/Atlas header strips).
3. **Live site audit** — `https://atlaslightingandhome.com/` (category tree, hero copy, featured products, footer columns, contact info).
4. **Reference site** — `https://sagebrookhome.com/` (dual-brand pattern — Sagebrook + Elevarre — used as model for the brand switcher).

## Audience UX class
**Older-B2B.** Driven by: wholesale-only audience (interior designers, dealers, retailers); customer's explicit "non-technical users" lean; the existing storefront's older buyer cohort. Result: 16px+ body, 52px primary buttons, no autoplay-only carousels, plain-language CTAs, persistent visible nav, brand-switcher tucked in account menu (not chrome).

## Preserved from the audit
- **Category tree** — Lighting (Indoor: Chandelier, Floor Lamp, Flush Mount, Mini Pendant, Pendant, Recessed, Sconce, Semi Flush Mount, Table Lamp, Vanity Light; Outdoor: Outdoor Flush Mount, Outdoor Pendant, Outdoor Wall Sconce, Post Light, Outdoor Table Lamp); Decor; Furniture; Outdoor Furniture; Thomas Lighting.
- **Hero copy & themes** — "Design in every detail" (Atlas), "Luxury minimalism" (Thomas, repurposed from existing Atlas hero rotation per the customer's reference to the existing hero box copy).
- **Featured product set** — Flora Grace, Noura, Chadwick, Fairfax, Diffusion, Abaca, Palacial, Rotunde, Starburst — all real chandelier names from the live site.
- **Contact info** — 1473 Yorkhouse Road, Rabun Gap, GA 30568; (762) 40-ATLAS / (762) 402-8527; sales@atlaslightingandhome.com.
- **Footer structure** — Products / Resources / About columns.
- **Brand assets** — both logos and the Thomas scrolling banner pulled directly from `Atlas & Thomas.xlsx → Assets`.

## Upgraded (against customer's 26-item issue list)
Every item below maps to a row in `Atlas & Thomas.xlsx` Sheet1:

| # | Issue | Resolution in this build |
|---|---|---|
| 1 | Use gray/white color for Atlas | `body[data-brand="atlas"]` palette: surface white/gray, ink primary, no color accent |
| 2 | Use Thomas blue (#366bab) for Thomas accents | `body[data-brand="thomas"]` uses `--brand-cta: #366bab`, navy primary |
| 3 | Background banner for Thomas brand | Thomas hero uses `assets/thomas-scrolling.png` as background |
| 4 | Font type and size — same on Thomas as Atlas | Single typography stack (Cormorant Garamond + Inter) shared across both brands |
| 5 | Brand switcher: move from top to dropdown, smaller, only show alternate brand, desktop only | Account dropdown contains `.brand-switch` showing only the alternate brand's logo + name |
| 6 | Remove social links from header | Header now has only logo, nav, search, wishlist, cart, account |
| 7 | Mobile view: brand logo in hamburger menu, below main brand name | Drawer `.drawer__brand` shows brand name on top, logo below |
| 8 | Thomas logo bigger in its header | `body[data-brand="thomas"] .logo-img{ height: 72px }` vs Atlas 52px |
| 9 | Homepage banner box (e.g., "luxury minimalism") moved to bottom of image | `.hero__inner{ justify-content: flex-end }` |
| 10 | Add "Collection" button in Thomas header | Thomas nav includes "Lighting by Collection" + "Collections" |
| 11 | Insert wishlist button on right side options (Thomas brand) | Wishlist icon present in header utilities (both brands; Thomas users get it as requested) |
| 12 | Category images stay within boxes; responsive at all zoom | Tiles use `background-size: cover; background-position: center` on a fixed-aspect `::before` pseudo-element — images can never overflow the tile |
| 13 | Remove "Explore Category" text → rename to "Featured Collections" on Atlas | Section heading literally "Featured Collections" |
| 14 | Shop Now buttons smaller than collection names | `.fc-card__title` 24px / `.fc-card__cta` 12px |
| 15 | Remove "lighting" small text from featured products | Product card has no category eyebrow above title |
| 16 | Featured products: 4 desktop, 2 mobile | `.fp-grid` 4 cols desktop, 2 cols mobile |
| 17 | Featured collections: 6 for Atlas (parity with Thomas) | Both brands render exactly 6 collection tiles |
| 18 | Category collage: Lighting LEFT, Furniture & Decor RIGHT | `.collage` 1.2fr/1fr — lighting spans left, furniture+decor stacked right |
| 19 | Footer: "Opportunity Buys" replaces "Clearance" | Footer Products column ends in "Opportunity Buys" |
| 20 | Rename "Tools and Resources" to "Resources" | Footer column heading is "Resources" |
| 21 | Add "Lighting by Collection" in Thomas header | First nav item on Thomas brand |
| 22 | Move filters to left side on PLP | `.plp__layout` 264px (filters) / 1fr (grid) |
| 23 | PLP: product names fully visible | `.pcard__title` 3-line clamp with reserved min-height — no mid-word cut |
| 24 | Product card: "Finish + Material" instead of "Size" concatenation | `.pcard__finish-material` row literally shows finish + material |
| 25 | Logged-out users: NO price and NO "Unlock Price"/"Login to See Price" — just blank | CSS: `body:not(.user-logged-in) .pcard__price-amount, .pcard__price-locked { display: none }`. No "Unlock" or "Login to see" pills exist in the DOM |
| 26 | PDP: item description more visible; add a small description after MOQ + price | PDP has a prominent `.pdp__short` block with brand-accent left border AND a `.pdp__price-note` below price |

## Defaults applied (Mode-D Easy template defaults)
- **Audience UX class:** older-B2B (auto, given trade audience).
- **Vertical preset:** lighting-trade (Atlas + Thomas are both lighting brands).
- **Structural reference:** sagebrookhome.com brand-switcher pattern (Sagebrook + Elevarre header logo pair).
- **Visual reference:** existing atlaslightingandhome.com.
- **Palette:** customer-supplied (`#f6f6f6` header bg, `#dddddd` feature bg, `#366bab` Thomas accent) — used verbatim.
- **Fonts:** "take from current site" — defaulted to Cormorant Garamond (display) + Inter (UI) since the live wordpress site doesn't expose a clean Google Fonts pairing. Confirm with customer.
- **Products per row:** 5 (per template field 9).
- **Products per page:** 50 (per template field 10).
- **Related products:** Yes (per template field 11).
- **Recently viewed:** Yes (per template field 12).
- **Pricing for logged-out:** Hidden, no "Unlock Price" pill (per issue 25).

## Assumptions flagged for customer
1. Hero copy uses live site language ("Design in every detail", "Luxury minimalism"). If you want fresh hero copy, swap in `BRANDS[name].heroTitle` in the JS.
2. Trade-show dates are plausible 2026 dates for High Point, AmericasMart, Dallas, Las Vegas Market. Replace with real booth assignments before going live.
3. Filler product cards (20-product PLP page) use real product names from the audit + procedurally generated SKUs. Replace with the real catalog feed.
4. Thomas content (story, collections list) is composed from publicly known Thomas Lighting heritage facts. Confirm phrasing with the customer before publishing.
5. Atlas logo asset in the XLSX is a different variant than the one on the live site — per the Assets sheet note. Confirm which is the official wordmark.
