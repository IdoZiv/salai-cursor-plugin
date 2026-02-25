---
name: salai-mcp
description: Use Salai MCP tools for smart cart, price comparison, product search, and grocery recommendations. Requires SALAI_API_KEY environment variable set from your Salai Profile.
---

# Salai MCP Skill

Use Salai MCP tools to build agentic workflows: search products, manage a smart cart, compare prices across Israeli retailers, and get recommendations.

## When to use

- Build a smart cart from product names or item codes
- Compare prices across Shufersal, Rami Levy, Victory, Yohananof
- Search products by Hebrew or English query (semantic search)
- Get complementary product recommendations
- Find the cheapest retailer for a list of items

## Setup

1. Get your API key from the Salai app: [app.salai.co.il](https://app.salai.co.il) → Profile → API Key → Generate
2. Set it as an environment variable in your shell profile (e.g. `~/.zshrc`):
   ```bash
   export SALAI_API_KEY="your-api-key-here"
   ```
3. The Salai MCP server will be available automatically after installing this plugin

## Tool overview

| Domain | Tools |
|--------|-------|
| **Search** | `autocomplete_products` (fast: use method `text` first, then `semantic` if no results), `search_products` (full RAG, Hebrew/English) |
| **Prices** | `get_product_prices`, `compare_prices`, `cart_of_israel` |
| **Stores** | `get_stores`, `get_retailers`, `get_my_store_context`, `set_my_selected_store` |
| **Carts** | `get_my_cart` (preferred), `get_cart`, `add_cart_item`, `update_cart_items`, `remove_cart_item`, `delete_cart`, `compare_my_cart` |
| **Recommendations** | `get_complementary_recommendations` |

## Workflows

### Smart cart (single cart per user)

1. `get_my_cart` (no args) — get or create the current user's cart
2. `autocomplete_products` with method `text` to resolve product names to `itemCode`; if no results, retry with method `semantic`
3. `add_cart_item` with the cart ID from step 1, plus `itemCode` and `quantity`
4. `get_my_cart` again to see updated cart with current prices
5. Optionally `compare_my_cart` to find the cheapest retailer for the full cart

### Price comparison

1. `compare_prices` with `items: [{ itemCode, quantity }]`
2. Returns prices per retailer for each item

### Cart of Israel

1. `cart_of_israel` — no arguments required
2. Compares the standard Israeli government basket across all retailers, with promotions and alternatives
3. Returns a ranked summary table (cheapest retailer first) and per-item breakdown

### Recommendations

1. `get_complementary_recommendations` with `itemCode` and `limit`
2. Returns products that pair well with the given item

## Edge cases

- **itemCode**: Use the canonical item code from search results (e.g. `7290027600007`). Always resolve via `autocomplete_products` before using `add_cart_item`.
- **Store context**: Use `get_my_store_context` to check if a store is selected. Use `set_my_selected_store` with `{ retailerId, storeId }` to set one.
- **Auth failures**: 401 means invalid or missing API key. Regenerate from Salai Profile if needed.
- **Cart ownership**: Each user has one cart. Use `get_my_cart` (no args) to get or create it.
- **Search scope**: `search_products` and `autocomplete_products` accept optional `retailerId` and `storeId` to restrict results to a specific store.
