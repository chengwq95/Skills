---
name: ecommerce-price-compare
description: Compare e-commerce offers and collect product/price evidence across one or more marketplaces. Use when a user asks to compare prices, check a shopping list or cart, find the cheapest trustworthy listing, collect product offers into a spreadsheet, or mentions 比价、查价格、哪家便宜、price comparison, Shopee, Lazada, Taobao, Amazon, or another marketplace. Verify selected variants on product pages, disclose price assumptions and evidence, and optionally create an Excel comparison.
---

# E-commerce price comparison

Turn a shopping list into an evidence-backed comparison. Work with any capable agent or browser: use the user's authenticated browser session when available; otherwise use permitted public web access. Never require a brand-specific agent, browser extension, or tool name.

## Scope and safety

- Confirm the delivery country/postcode, currency, quantity, condition (new/used/refurbished), and required exact variant when they materially affect the result. If unavailable, use clearly labelled assumptions.
- Do not log in, enter credentials, place orders, add items to carts, redeem coupons, start a checkout, or contact sellers without the user's explicit approval. Ask the user to complete any login or CAPTCHA themselves.
- Follow site terms, robots restrictions, rate limits, and available tools. Do not bypass access controls, CAPTCHAs, or anti-bot measures.
- Treat a listing as a lead—not a confirmed offer—until its product page and selected variant have been checked.

## Collect offers

For each requested product, first define a comparison key: brand/model, capacity or size, colour/connector/version, quantity, condition, and any must-have compatibility feature. Do not group offers with different keys.

Search each requested marketplace. When practical, include an official/authorised retailer and a reputable third-party retailer. Prefer sellers with clear return policies, strong ratings and meaningful sales history. Flag rather than silently include offers that appear counterfeit, incomplete, pre-order, misleadingly bundled, or implausibly cheap.

Open each candidate product page and select the exact required variant. Record:

- full title, marketplace, seller, selected variant, condition, availability, and product URL;
- item price and currency; shipping, tax/duty, and discount only when shown and applicable to the user's location/eligibility;
- price type: listed, variant-selected, member price, coupon price, checkout estimate, or unavailable;
- capture time and a short evidence note (for example, page text or screenshot reference).

If a value cannot be verified, use `unknown`; never infer it from a search-result card, an unselected price range, another variant, or an expired promotion. A displayed out-of-stock price may be retained as historical context, but exclude it from the buy-now winner.

## Decide what is comparable

Use a single currency for a ranked comparison. If conversion is needed, record the exchange-rate source and time; do not mix currencies without conversion. Compare the best available "comparable total":

`item price + required shipping + known tax/duty - guaranteed applicable discount`

Only call an offer the cheapest when the comparison key and price basis match. If shipping, tax, discount eligibility, membership, or delivery destination is unknown, rank by verified item price only and label the conclusion provisional. Show ties and material non-price trade-offs (delivery time, warranty, return policy, seller trust).

## Produce the deliverable

Give the user a concise recommendation and link each supporting product page. State the capture time, delivery-location assumption, currency, whether the winner is in stock, and every caveat that could change the recommendation.

When an `.xlsx` file is useful, create these three sheets:

1. **比价明细** — one offer per row, including evidence URL and price components.
2. **比价汇总** — one comparison key per row; list the best eligible offer per marketplace and the current winner or `需人工确认`.
3. **说明** — assumptions, capture time, currency/FX source, price basis, exclusions, and unresolved fields.

Use `scripts/build_price_excel.py` for the standard workbook. Supply JSON as described by `--help`. It accepts the original simple `price` format for compatibility, but an offer needs `comparison_price` or all price components before it can become a current winner. Read the generated workbook back and verify every amount, selected variant, availability, link, and winner against the recorded evidence before delivery.

## Capability adaptation

- **Authenticated browser available:** ask the user to log in themselves, then inspect the real variant and location-specific shipping where permitted.
- **Public browser/search only:** gather public product-page evidence; label cart, voucher, member, and delivery estimates unavailable unless visible.
- **No browsing capability:** do not fabricate current prices. Ask for URLs, screenshots, or exported cart data, then normalise and compare the supplied evidence.
- **Spreadsheet capability unavailable:** return a Markdown table with the same fields; do not claim an Excel attachment exists.

## Quality gate

Before responding, ensure every winner has: an exact comparison key, a selected-variant product-page URL, a currency, an availability state, a stated price basis, and no unlabelled missing shipping/tax/discount assumption. Otherwise downgrade the conclusion to provisional or `需人工确认`.
