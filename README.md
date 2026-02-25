# Salai – Cursor Marketplace Plugin

Compare grocery prices across Israeli retailers, build smart carts, and get recommendations — directly from Cursor.

## What this plugin does

- **Search products** in Hebrew or English across Shufersal, Rami Levy, Victory, and Yohananof
- **Compare prices** for individual items or a full cart across all retailers
- **Build a smart cart** and find the cheapest store to shop at
- **Cart of Israel** — one-shot comparison of the standard Israeli grocery basket with promotions
- **Recommendations** — get complementary product suggestions

## Setup

### 1. Get your Salai API key

1. Sign in at [app.salai.co.il](https://app.salai.co.il)
2. Go to **Profile → API Key → Generate**
3. Copy the key (it's shown only once)

### 2. Set the environment variable

Add to your shell profile (`~/.zshrc`, `~/.bashrc`, etc.):

```bash
export SALAI_API_KEY="your-api-key-here"
```

Then reload: `source ~/.zshrc`

### 3. Install the plugin in Cursor

Install from the [Cursor Marketplace](https://cursor.com/marketplace) or add manually to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "salai": {
      "url": "https://mcp.salai.co.il/mcp",
      "headers": {
        "Authorization": "Bearer your-api-key-here"
      }
    }
  }
}
```

## Available tools (17)

| Category | Tools |
|---|---|
| Search | `search_products`, `autocomplete_products` |
| Prices | `get_product_prices`, `compare_prices`, `cart_of_israel` |
| Stores | `get_stores`, `get_retailers`, `get_my_store_context`, `set_my_selected_store` |
| Carts | `get_my_cart`, `get_cart`, `add_cart_item`, `update_cart_items`, `remove_cart_item`, `delete_cart`, `compare_my_cart` |
| Recommendations | `get_complementary_recommendations` |

## Example prompts

- `"Add milk, eggs, and bread to my cart"`
- `"Compare prices for my cart across all stores"`
- `"Run the Cart of Israel comparison"`
- `"Search for חלב 3% שטראוס"`
- `"What goes well with pasta?"`

## Links

- [Salai app](https://app.salai.co.il)
- [MCP server](https://mcp.salai.co.il/mcp)
- [Support](mailto:support@salai.co.il)
