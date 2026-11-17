# Tether documentation agent instructions

This is the help site for **Tether**, a supply chain planning app: demand planning, inventory, supply planning (purchase, transfer and production recommendations), orders, and integrations. Pages are MDX, rendered by Mintlify at docs.tetherdata.io.

## Who reads these pages

Two readers, and the second one matters most:

1. **People using Tether**, who browse or search the site.
2. **Tether's in-app agent**, which answers user questions by searching this site. The search returns about five short excerpts (one heading's section each), never the whole page. The agent only knows what's inside the excerpts it gets.

So every how-to section must make sense on its own, starting with where it is in the app.

## Source of truth

- The app's code is the source of truth for every screen name, tab, button label and path. The sidebar is defined in `clients/erp/src/shared/navigation/nav-registry.tsx` in the tether repo. Check a label there (or in the page's component) before you write it.
- Never describe a control you haven't seen in the code or the app.
- If a feature is only on for some orgs (a feature flag, or the newer catalog and locations model), say so: "If you don't see **Lots**, ask Tether to turn on lot tracking."
- Orgs can rename some terms in **Settings → Terminology** (for example SKU Group, Location). Write the default term.

## Page structure

1. **Frontmatter:**
   - `title`
   - `description`: what the page lets you do and where it is in the app, in the words a user would search with. Example: `description: "Where: Products → SKUs → a SKU → Cost & price. Set a SKU's Default cost, see its Standard cost and set sales prices."`
   - `sidebarTitle` (optional)
2. **Intro:** one or two sentences on what the screen is for.
3. **One H2 per task or question.** Each one:
   - starts with a `Where:` line giving the full path, e.g. `**Where:** Supply Chain → Purchase → List → Suggested`
   - uses the user's words as the heading ("Why didn't Tether recommend a purchase?", "Release a held order")
   - gives short numbered steps or a `<Steps>` block, with on-screen labels in bold
4. **Troubleshooting** (optional): the symptom as the heading, then the cause and fix.

Leave out "Next steps" card grids and generic "Best practices" sections. They push real answers out of the agent's top results. Link related pages inline instead.

## Terminology

Use the term the app shows today. When a page replaces an older term, mention the old word once ("Locations, formerly Warehouses and Suppliers") so searches using it still find the page.

| Concept | Use | Don't use |
|---|---|---|
| Sidebar group for SKUs, SKU Groups, BOMs and Attributes | **Products** | Principal Catalog |
| Legacy catalog screens (Collections, /skus), only on older orgs | **Catalog** (say it's the older screen) | Product Catalog as the default |
| What one unit of a SKU costs when no supplier or site has its own price | **Default cost** (a SKU → **Cost & price**) | unit cost |
| Cost Tether works out per SKU: purchase price for bought SKUs, components plus production cost for made ones | **Standard cost** | |
| What a SKU sells for | **Sales price** | list price, pricing tab |
| Plan of upcoming supply | **Supply Plan** (Supply Chain → Supply Plan) | Execution plan |
| Planning across demand and supply | **Connected Planning** | |
| When the planning engines ran | **Engine runs** | solve history (except the settings page of that name) |
| Rules that shape recommendations (MOQ, multiples, lead time) | **Policies** | constraints, SKU settings |
| Warehouses, suppliers, factories, 3PLs | **Locations** (Supply Chain → Locations) | Warehouses, Nodes |
| A suggested purchase, transfer or production run | **recommendation** | suggestion |
| Turning down a recommendation | **reject** (with a reason) | dismiss, snooze |
| Sales order status: Tether hasn't sent it to the warehouse yet | **Held by Tether** (a Status filter on Sales → Orders) | on hold |
| Checking in arrived goods | **Receiving** | |
| Scheduled agent reports | **Standing reports** | |
| Stock Keeping Unit | **SKU** (uppercase) | Sku, sku |
| Running out of stock | **stockout** | stock-out |
| Excess inventory | **overstock** | over-stock |
| Minimum inventory threshold | **safety stock** | safety-stock |
| Time to receive goods | **lead time** | lead-time |
| Order types | **Purchase Order**, **Transfer Order**, **Production Order** | |
| Verb vs noun | **set up** (verb), **setup** (noun) | |
| Spelling | American English: fulfill, optimize | fulfil, optimise |

## Sections

| Section | Path prefix | App area |
|---|---|---|
| Getting started | `/` | Home, quickstart, sidebar map, roles |
| Agent | `/agent/` | Agent: Chat Sessions, Standing reports, agent settings, connectors |
| Demand | `/demand-forecasting/` | Demand: dashboard, Comparison, Season Plan, Edit Log, Admin |
| Marketing & Promotions | `/marketing-promotions/` | Drivers, Promotions, Price Calendar |
| Inventory | `/inventory/` | Inventory: dashboard, Locations, Suppliers, Lots |
| Orders | `/transactions/` | Transactions, Review lists, Shipments |
| Supply planning | `/supply-planning/` | Supply Chain: Policies, Connected Planning, Transfer, Production, Purchase, MRP, Supply Plan |
| Products | `/principal-catalog/` | Products: SKUs, SKU Groups, BOMs, Attributes |
| Catalog (legacy) | `/product-catalog/` | Catalog: Collections, SKUs on older orgs |
| Sales | `/channels/`, `/sales/` | Sales: Sales Channels, Orders, Sales History |
| Integrations | `/integrations/` | Settings → Integrations |
| Settings | `/administration/` | Settings pages |
| Tips | `/tips/` | Command palette, shortcuts, exports |

## Mintlify basics

- Run `mint dev` to preview and `mint broken-links` before every PR.
- Components: https://www.mintlify.com/docs/components. Use `<Steps>`, `<Note>`, `<Tip>`, `<Warning>`, and tables for reference data.
- Links: root-relative, no `.mdx`: `[Policies](/supply-planning/policies)`.

## Moving or removing pages

- Before you remove a page, grep for links to its path and fix them.
- Add a `redirects` entry in `docs.json` from the old path to the page that replaces it, so old links and the agent's cached URLs still land.
- Only add pages to `docs.json` navigation once the `.mdx` file exists.

## Keeping the docs current

Each week's release notes (`release.src.md` in the tether repo) list the shipped features. Each feature names its docs page, the old wording that page replaces, and a few questions users will ask. One docs PR per week follows from that list. It's done when each of those questions, searched on the docs site, returns the right page in the top three results.
