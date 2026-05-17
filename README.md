# Mohsin Collection — Premium Custom Shopify OS 2.0 Theme

A bespoke, lightweight storefront engineered from the ground up using vanilla HTML, CSS, Liquid, and JavaScript. This theme rejects the bloat of marketplace templates in favor of sub-second load times, granular UX control, and a "Midnight Luxury" design system tailored specifically for high-ticket, business-class consumers.

---

## 💎 Architectural Philosophy: Systems Over Products

This storefront is architected as a **psychological filtering system** to elevate the brand asset value and completely eliminate traditional retail bargaining friction:

* **Space-Forward Layouts:** Heavy whitespace ratios signal premium pricing and exclusivity, separating the collection from cluttered mass-market grids.
* **Empirical Valuation Transparency:** Hardcoded technical specification grids present jewelry weights and purity certifications as immutable physical facts rather than fluid retail metrics.
* **Concierge Acquisition Vectors:** High-ticket items bridge directly into personalized WhatsApp Design Consultation streams to capture upper-middle-class leads through high-touch service pipelines.

---

## 🎨 Design Token Specifications

The visual interface utilizes a soft-contrast, luxury-dark configuration to allow high-resolution jewelry photography to stand out vibrantly on mobile displays.

* **Background (Midnight Space):** `#12131f`
* **Primary Accent (Light Gold Text):** `#fde688`
* **Muted Trim / Borders (Deep Bronze):** `#975e29`
* **Body Content Layer (Warm Cream):** `#f7f5f0`
* **Typography Scale:** `Cinzel` / `Playfair Display` (Headings) | `Inter` (Functional Body / Metadata)

---

## 📂 Directory Architecture Map

The repository conforms strictly to the Shopify Online Store 2.0 theme standard:

```text
├── assets/
│   ├── custom-style.css.liquid   # Compiled global luxury design tokens & layouts
│   └── mohsin-core.js            # Core interactive states and UI scripts
├── config/
│   ├── settings_data.json        # Schema data assignments and current state configurations
│   └── settings_schema.json      # Dynamic inputs mapping schema for the Shopify Editor panel
├── layout/
│   └── theme.liquid              # Master HTML document wrapper and engine hooks
├── locales/
│   └── en.default.json           # Structural interface translation string matrix
├── sections/
│   ├── footer.liquid             # Bottom brand footprint, trust metrics & copyright definitions
│   ├── header.liquid             # Sticky, minimalist top navigation bar
│   ├── main-collection.liquid    # Dynamic item loop layout engine for catalog routes
│   └── main-product.liquid       # High-value product detailing page with contextual actions
├── snippets/
│   ├── card-product.liquid       # Modular catalog preview listing tile
│   ├── icon-whatsapp.liquid      # Scalable Vector Graphic token for concierge triggers
│   └── product-specifications.liquid # Explicit validation metrics grid
└── templates/
    ├── cart.json                 # Transaction route schema mapping layout
    ├── index.json                # Primary Homepage grid configuration map
    └── product.json              # Direct Product listing dynamic layout index

```

---

## ⚙️ Data Layer Requirements (Shopify Metafields)

To power the empirical validation specifications table without hardcoding individual item data, the following Custom Data Fields **must** be generated in the Shopify Admin interface:

1. Navigate to **Settings > Custom Data > Products > Add Definition**.
2. Configure these four definitions with exact keys:

| Field Label | Namespace & Key | Data Type | Purpose |
| --- | --- | --- | --- |
| **Purity Certification** | `custom.purity` | Single line text | e.g., "22K BIS Hallmarked Gold" |
| **Gross Weight** | `custom.gross_weight` | Single line text | Total mass including settings (e.g., "14.25g") |
| **Net Gold Weight** | `custom.net_weight` | Single line text | Pure alloy mass calculation (e.g., "12.80g") |
| **Gemstone Settings** | `custom.stone_details` | Multi-line text | Cut, clarity, and stone allocations |

---

## 🚀 Deployment Instructions

Because this codebase bypasses continuous deployment middleware to keep workflows clean, it can be packaged and deployed directly into production via the Shopify Admin Dashboard.

### Step 1: Compile the Source Package

1. On your machine, open the root theme directory containing your assets, layouts, and templates.
2. Select all folders (`assets`, `config`, `layout`, `locales`, `sections`, `snippets`, `templates`).
3. Compress the selected directories into a single standard `.zip` file. Name it `mohsin-collection-production.zip`.

### Step 2: Push into Production

1. Authenticate into the **Shopify Admin Dashboard**.
2. Using the left-hand navigation pane, head to **Sales Channels > Online Store > Themes**.
3. Locate the *Theme Library* container matrix.
4. Click the **Add Theme** selector dropdown, then click **Upload zip file**.
5. Drag and drop `mohsin-collection-production.zip` into the modal and click **Upload**.
6. Once processing finishes, select **Actions > Publish** next to your uploaded package to take the custom storefront live.

---

## 🛠️ Production Verification Maintenance

* **To Alter Content Language Strings:** Edit `locales/en.default.json` directly to change globally distributed text (such as replacing "Secure This Piece" with alternative luxury strings).
* **To Update Styling Layouts:** Add pure CSS definitions inside `assets/custom-style.css.liquid` directly underneath the variable architecture block. Use root tokens (`var(--text-gold-light)`) to retain color parity across elements.
