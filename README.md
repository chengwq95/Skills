# E-commerce Price Compare

An evidence-backed e-commerce price-comparison skill for AI agents. It helps turn a shopping list into a trustworthy comparison across marketplaces such as Shopee, Lazada, Taobao, and Amazon.

## Package

- `ecommerce-price-compare.skill` — installable skill package with the workflow and Excel workbook builder.

## What it does

- Verifies the exact selected variant on the product page rather than trusting search-result price cards.
- Records seller, availability, price type, delivery assumptions, taxes, discounts, currency, and source URL.
- Compares like-for-like offers only and marks incomplete prices as provisional.
- Flags likely counterfeit, misleading, pre-order, or unavailable listings.
- Produces a three-sheet Excel comparison when spreadsheet support is available.

## Example requests

- “Compare the price of this 1TB SSD on Shopee and Lazada in Malaysia.”
- “Find the cheapest trustworthy listing for these items and include shipping.”
- “Turn these product links into a price-comparison spreadsheet.”

## Key safeguards

The skill does not enter credentials, bypass CAPTCHAs, place orders, redeem coupons, or contact sellers without explicit permission. If shipping, tax, coupon eligibility, or exchange-rate information cannot be verified, it is disclosed instead of being guessed.

## Installing

Download `ecommerce-price-compare.skill` and import it into an agent platform that supports Skill packages. The workflow is capability-based, so it can work with an authenticated browser, public browsing tools, or user-supplied links and screenshots.
