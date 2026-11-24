# Menu change: fudge brownies replace cake pops

Instructions for the Claude session that has the website code. Swap the
**vanilla & chocolate cake pops** for **fudge brownies** in the menu.

## What to change

- **Remove:** vanilla & chocolate cake pops (slug `vanilla-chocolate-cake-pops`).
  They're one of the three every-month favorites in `data/monthly-menu.ts`.
  Also check `/menu/vanilla-chocolate-cake-pops`, the order form, and any
  links to that page. Redirect the old page to the new one if that's simple.
- **Add:** fudge brownies, in the same every-month favorites slot.

| Field | Value |
| --- | --- |
| Name | fudge brownies |
| Slug | `fudge-brownies` |
| Photo | `public/products/fudge-brownies.png` (in this branch, transparent background, 1200×900 like the other product photos) |
| Sizes sold | **half dozen (6)** and **dozen (12)** — no single brownies |
| Prices | **ASK THE OWNER** — not decided yet |
| Hover color | **teddy bear brown** — use the site's existing `teddy` color, with a chocolate-chip touch (e.g. small chocolate-chip dots in the card decoration, `components/CardDecor.tsx`) |

## Recipe (one 8×8 pan = 12 brownies)

- ½ cup unsalted butter (1 stick, 113 g)
- ¾ cup granulated non-sugar sweetener, cup-for-cup baking type (about 150 g)
- 2 large eggs
- ½ cup unsweetened cocoa powder (40 g)
- ½ cup all-purpose flour (about 65 g)
- ¼ teaspoon fine salt
- 1 teaspoon vanilla extract
- ⅓ cup **regular** semi-sweet chocolate chips (55 g), divided

## Nutrition (estimate, per brownie, 12 per pan)

- About **135 calories**
- About **3 g sugar**, all from the chocolate chips

These are estimates from typical labels. Recalculate from the actual
product labels before printing exact numbers.

## Wording rules

- **Don't call the brownies "no added sugar" or "sugar-free".** The
  chocolate chips are regular, so they contain sugar. Check that nothing
  on the site says *every* bake is no added sugar (the About page has a
  "no added sugar" badge, `public/about/no-added-sugar.*`). Reword it, or
  leave the brownies out of that claim.
- **Don't call them gluten-free or keto.** They use all-purpose flour.
- Allergens to list: **wheat, eggs, milk** (butter, and usually the
  chocolate chips), and **soy** if the chips' label lists soy lecithin.

## Check before going live

1. `npm run build` passes.
2. Deploy a preview. Check the home page, `/menu`, `/menu/fudge-brownies`
   and `/order`, and that both sizes can be ordered at the right prices.
3. Check that the cake pops are gone everywhere.
4. Promote to production and check faithandflour22.com.
