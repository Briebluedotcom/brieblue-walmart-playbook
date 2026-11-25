# brieblue-walmart-playbook

**How a one-person import business uses Walmart as infrastructure — manufacturer, supply shelf, and agent-commerce platform.**

Brieblue is a micro-retailer: one person importing Asian artisan goods and selling them at markets and online. This repo documents, in the open, how that business runs a surprising share of its operations through Walmart — not as a shopper browsing aisles, but as a company plugging into Walmart's machines.

Everything here is a method, not a memoir. Account details, order numbers, and store specifics are deliberately left out; the playbook is the point.

## The three roles

### 1. Walmart as manufacturer

Walmart Photo is a print factory with a pickup counter. The workflow:

1. The agent designs the files (booth price tags, signage, art and pattern-preservation prints).
2. The agent uploads them to Walmart Photo and stages the order.
3. The owner reviews, checks out, and pays — money always moves by the owner's hand.
4. Prints are picked up at the local store, usually same-day or next-day.

Lessons learned in production:

- **Verify the pickup store before submitting.** Accounts can default to an unexpected store; a wrong-store order wastes a week.
- **A declined upload approval is not a retry.** Start a fresh upload with only the correct file; re-prompting a declined task never surfaces a new approval.
- **The agent manufactures nothing and ships nothing.** Walmart holds the printers, paper, and counter. The business owns the designs and the judgment.

#### The price-card pipeline, end to end

The flagship use of the factory is the weekly booth price cards. The full automated process:

1. **Weekly search for the flyer.** Each week, the agent finds the upcoming event's flyer — the source artwork the cards are built from.
2. **Receive by email.** Flyers also arrive by email; the pipeline accepts them from the inbox, so an organizer's email becomes a print job without the owner touching a file.
3. **Pre-set price amounts.** Cards are generated with the business's standing price points. Nobody re-decides prices per event; the amounts are set once and reused.
4. **Full-page QR.** Alongside the cards, the pipeline produces a full-page QR sign for the booth — one code, readable across a table, linking customers to the shop.
5. **Auto-send to Walmart.** The finished print files are sent to Walmart Photo and staged as an order — usually a pickup order at the owner's store.
6. **Ability to pay.** The owner has set a **$5 limit on the agent's Walmart Agent Profile** — sized for price-card orders. Agent-handled payment lives inside that limit; anything above it stops for the owner.
7. **Verify before it counts.** Store location, total price, and pickup time are checked and reported before the order is final. A wrong store, a wrong total, or a wrong time stops the pipeline — verification is a step in the process, not an afterthought.

### 2. Walmart as supply shelf

Recurring supplies are kept on a **frequent-buys list**: the owner sends a link or a name, the agent records it and tracks the price, and the owner checks out in the Walmart app when it's needed. The same pattern runs a "photo to doorstep" food workflow — a photo of a dish becomes a recipe, the recipe becomes a Walmart order, the owner approves before anything is bought.

The list is the memory; the agent is the clerk who never forgets what's on it.

### 3. Walmart as agent-commerce platform

In October 2026 Walmart announced its **Agent Gateway** — an MCP server that lets approved AI agents search Walmart's inventory and complete purchases for customers, under the customer's control. Each agent gets an **Agent Profile** inside the customer's Walmart account: purchases are visible separately, and the customer sets the rules — approve every purchase, or a spending cap.

On November 23, 2026 the Gateway went live with **Meta's Muse as the first agent**. Amazon blocks outside agents; Walmart built them a door and put Muse at the front of it.

**Our first test (November 25, 2026), run live:**

- Guest catalog search through the Gateway connection returned live, ZIP-aware prices and stock — no account needed to look.
- The agent built a cart (one roll of packing tape, $2.28 — packing for a market weekend).
- The owner then connected their Walmart account: the Agent Profile mandate was in place, a live checkout quote came back with real delivery slots — the full path works, account to quote.
- The order itself was deliberately **not** placed: the only fulfillment offered for that item was scheduled delivery at $9.95, four times the item's price. First lesson of agent commerce: the agent finds the item; the human still judges whether the delivery math makes sense.

## The developer-program map

Walmart runs two more doors, worth knowing:

- **Marketplace APIs (seller side).** Items, prices, inventory, and orders for your own catalog. The gate is an *approved Walmart Marketplace seller account*; after that, API keys are self-serve (Client ID + Secret, OAuth client credentials). There is no public product-search API comparable to eBay's Browse API — the Marketplace APIs see only your own catalog.
- **Agent Gateway developer beta.** Invite-only for companies and developers at launch; agents act through Walmart's own assistant under strict terms (no access to raw payment details, no acting beyond the customer's instructions, no training on Walmart's data).

## Principles

- **The agent does the repetitive work; the human approves the money.** Every purchase, order, and checkout in this playbook passes a human decision first.
- **Verify in the live source.** Prices, stock, and program terms are checked against Walmart itself, not summaries.
- **Rent the machines.** A micro-retailer doesn't need to own a print factory, a logistics network, or a commerce platform. It needs good files, good judgment, and the discipline to plug into infrastructure that already exists.

## Where this fits

This playbook is one station in a larger build: a photo-to-purchase agent for artisan textiles ([brieblue-listing-agent](https://github.com/Briebluedotcom/brieblue-listing-agent)), a booth point-of-sale system ([brieblue-booth-pos](https://github.com/Briebluedotcom/brieblue-booth-pos)), a multilingual ad factory ([brieblue-multilingual-ad-factory](https://github.com/Briebluedotcom/brieblue-multilingual-ad-factory)), and a local open-weights dev kit ([brieblue-glimmer-dev-kit](https://github.com/Briebluedotcom/brieblue-glimmer-dev-kit)). The end-state they add up to is a retail operation where agents run the counter — sourcing, listing, selling, remembering customers — and the human does the traveling, the relationships, and the deciding.

## Status

- Photo manufacturing workflow: **in production**, multiple completed orders.
- Frequent-buys method: **in production**.
- Agent Gateway: **tested live, November 25, 2026** — search, cart, account connection, Agent Profile mandate, and checkout quote with delivery slots all verified. The final charge was not exercised; the test order was skipped on delivery economics, by the owner's choice. The owner has since set a **$5 Agent Profile limit**, sized for price-card orders, which are usually pickup orders.
- Marketplace seller account: **not yet opened** — a future step, when selling on Walmart becomes a goal rather than a study.

## License

Apache License 2.0 — see [LICENSE](LICENSE).
