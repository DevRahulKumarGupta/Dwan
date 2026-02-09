# Custom Related Products Section (Shopify OS 2.0 / Dawn)

Production-ready **Related Products** section for product pages (built for **Dawn**) with a clean, modern card UI and responsive layout:
- **Desktop:** grid layout
- **Mobile:** horizontal slider/scroll
- **Performance:** lazy-loaded images, minimal JS, no third-party apps

---

## Features

### Product sourcing options
This section supports three ways to select related products:

1. **Product metafield (recommended)**
   - Reads a product metafield of type **List of products**
   - Gives precise control per product

2. **Collection**
   - Displays products from a selected collection

3. **Manual selection**
   - Select up to 10 products directly from the theme editor

### Theme editor settings
- Section heading
- Products to show (range setting)
- Products per row (desktop/tablet)
- Toggle price visibility
- Toggle Add to Cart button
- Optional vendor + sale badge
- Layout controls (padding, container width, gap)
- Color + typography controls

### Add to cart behavior
- Uses Shopify’s native `/cart/add.js` endpoint (AJAX)
- Falls back to Shopify cart/checkout flow handled by the platform and Dawn

---

## Installation

1. Copy the section file into your theme:
   - `sections/custom-related.liquid`

2. Open the theme editor:
   - **Online Store → Themes → Customize**

3. Navigate to a product page template:
   - Example: `Products → Default product`

4. Click **Add section**
   - Select **Custom related products**

5. Configure product source (recommended: metafield)

---

## Metafield setup (Recommended)

### Step 1: Create the metafield definition
Go to:
- **Settings → Custom data → Products → Add definition**

Use:
- **Name:** Related products  
- **Namespace:** `custom`  
- **Key:** `related_products`  
- **Type:** **List of products**

> The section expects a metafield type of **List of products**.

### Step 2: Assign related products
Open a product in admin:
- **Products → [Product]**
- Add values in the **Related products** metafield field

### Step 3: Configure section settings
In the section settings:
- Product source: **Product metafield**
- Namespace: `custom`
- Key: `related_products`

---

## Using collection source

1. In the section settings:
   - Product source: **Collection**
   - Select a collection (example: “Speakers”)

2. The section will render products from that collection (up to the selected limit).

---

## Using manual selection

1. In the section settings:
   - Product source: **Manual selection**
   - Select products (up to the editor limit)

---

## Notes on login → checkout → payment flow

This section is part of the product page experience and supports:
- Browsing related items
- Adding items to cart (AJAX)
- Continuing to cart/checkout using Shopify + Dawn’s built-in flow

Shopify handles:
- Customer login (optional / depends on store settings)
- Checkout and payment processing
- Order confirmation

No third-party apps or custom payment scripts are required or used.

---

## File structure

- `sections/custom-related.liquid`  
  Contains:
  - Liquid logic for sourcing related products
  - Section styles (scoped per section instance)
  - Markup for desktop grid + mobile slider
  - Add-to-cart JavaScript (AJAX)

---

## Implementation logic (High-level)

1. Determine product source from theme settings:
   - metafield / collection / manual
2. Resolve `products_to_show`
3. Render cards with:
   - image (lazy-loaded)
   - title
   - optional vendor
   - optional price (with compare-at sale state)
   - optional add-to-cart (variant ID: `selected_or_first_available_variant.id`)
4. Render:
   - Desktop grid for larger screens
   - Scroll slider for mobile

---

## Compatibility

✅ Shopify Online Store 2.0  
✅ Dawn theme (tested approach: Liquid + native cart endpoints)  
✅ No third-party apps

