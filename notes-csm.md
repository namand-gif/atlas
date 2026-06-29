# Atlas & Thomas — CSM talking points

## One-paragraph rationale
We rebuilt the storefront as a single responsive site with a clean brand switcher tucked into the account menu — exactly like Sagebrook Home does with Elevarre. Atlas keeps its gray-and-white feel; Thomas gets a navy + #366bab accent and its scrolling banner. We preserved the category tree, the founder address, the contact details, and the existing hero language, and worked through every one of the 26 issues from your feedback sheet — from "filters on the left of the PLP" down to "no Unlock Price button for logged-out users."

## What we preserved
- All category names and the navigation hierarchy from `atlaslightingandhome.com`
- Footer columns (Products / Resources / About) and the contact block (Rabun Gap, GA + phone + email)
- Featured product names from the live site (Flora Grace, Noura, Chadwick, Fairfax, etc.)
- The Atlas hero phrasing ("Design in every detail") and the Thomas "Luxury minimalism" line
- Both brands' assets you supplied in the spreadsheet

## What we upgraded (mapped to your feedback)
- **Brand switcher moved from a top toggle to a small alternate-brand button inside the account dropdown** (issue 5) — desktop only.
- **Header simplified**: social icons removed (issue 6); Thomas logo enlarged (issue 8); wishlist icon kept visible (issue 11); "Lighting by Collection" added on Thomas (issue 21).
- **Mobile drawer redesigned** with brand name on top and brand logo below it, so the logo is inside the menu, not the chrome (issue 7).
- **Hero copy box moved to the bottom of the image** (issue 9) and shaped as a frosted-glass card.
- **"Explore Category" renamed to "Featured Collections"** with 6 tiles (issues 13, 17) and a smaller Shop Now pill so the collection name reads first (issue 14).
- **Category collage flipped**: Lighting takes the larger left tile, Furniture + Decor stack on the right (issue 18). Images are locked to fixed-aspect tiles so they can never overflow at any zoom (issue 12).
- **Featured Products row is 4 on desktop, 2 on mobile** (issue 16) — no "lighting" eyebrow above the title (issue 15).
- **Product card cleaned up**: 3-line title clamp so names never get cut off (issue 23); finish + material replaces the old size concatenation (issue 24); **the entire price area is hidden for logged-out users — no "Unlock Price" or "Login to See Price" pill** (issue 25).
- **PLP filters moved to the left**, sticky as the buyer scrolls (issue 22); 5-up grid; 50 products per page.
- **PDP description** is now a prominent paragraph block with a brand-accent left bar (issue 26); a one-line note appears below MOQ + price summarizing volume discounts and warranty (issue 26).
- **Footer**: "Tools and Resources" renamed to "Resources" (issue 20); Atlas footer now has "Opportunity Buys" in place of Clearance (issue 19).

## Customer demo flow (suggested 8-minute walkthrough)
1. **Open the site as a logged-out visitor.** Walk through the homepage. Highlight: no prices anywhere (issue 25), banner box at the bottom of the hero (issue 9), 6-tile Featured Collections (issue 17), the new collage with Lighting on the left (issue 18).
2. **Click the account icon → "Switch to Thomas Lighting."** Show how the entire header, logo, palette, hero, and content flip — that's the same pattern Sagebrook uses with Elevarre, exactly as you asked.
3. **On Thomas: scroll the homepage.** Point out the bigger logo (issue 8), the navy + blue palette (issue 2), the Thomas scrolling banner behind the hero (issue 3), the "Lighting by Collection" nav (issue 21), and the wishlist icon (issue 11).
4. **Click Shop / open the PLP.** Show filters on the left (issue 22), 5-up grid, names not cut off (issue 23), finish+material below SKU (issue 24).
5. **Click a product to open the PDP.** Show the prominent description block (issue 26), MOQ + price + small description note (issue 26), variant tiles, 4 accordions, related + recently viewed.
6. **Click Sign in (top right).** Submit any email/password. After sign-in: prices, MOQ, and Add-to-Cart appear everywhere. The cart badge increments when you add.
7. **Switch back to Atlas.** Footer now shows Opportunity Buys (issue 19) and Resources (issue 20).
8. **Resize the browser to ~375 px** to demo the mobile drawer (issue 7) and the 2-up Featured Products grid (issue 16).

## Comparison summary (vs current site)
- **Visual register.** Today: lots of small UI metal and tight type. Now: bigger body text, larger CTAs, cleaner hierarchy — friendlier for older trade buyers.
- **Brand differentiation.** Today: Thomas content lives inside the Atlas chrome. Now: a true dual-brand switch flips header, footer, palette, hero, and content.
- **Pricing affordance.** Today: "Unlock Price" / "Login to See Price" pills. Now: silent gating — the price area is simply empty until sign-in (your call, issue 25).
- **PLP usability.** Today: top-bar filters; some product names truncate. Now: left-sidebar filters; 3-line clamp guarantees the title is always readable.
- **PDP description.** Today: short summary buried below variants. Now: a highlighted paragraph block with a brand-color left bar, before the price.

## 5 questions to finalize before launch
1. **Which Atlas wordmark do we treat as canonical?** The XLSX has one variant; the live site has another.
2. **Hero photography for Atlas** — do you have a banner you'd like used, or should we commission?
3. **Real product catalog feed** — when can we point the PLP at the live `/products` endpoint? Need SKU + name + finish + material + MOQ + case pack + image URL + category for ~500–2,000 lines.
4. **Booth assignments for 2026** — confirm the dates and booth numbers we used or replace with the real schedule.
5. **Designer trade program** — do you want a dedicated landing page in v1, or just a footer link to the existing PDF for now?
