# Mohsin Jewelers — Real-Time Mobile Showroom & Pocket Catalog

A zero-overhead, mobile-first digital showroom and real-time inventory system engineered by **Sapphire Systems** for **Mohsin Jewelers** (Old City, Hyderabad). Built to bridge Instagram Reels, YouTube Shorts, and WhatsApp forwards directly into verified WhatsApp enquiries and physical showroom visits—running on a ₹0/month serverless stack with zero weekday maintenance.

---

## 💎 Architectural Philosophy: Frictionless Counter Ops & Social Proof

This application rejects bloated e-commerce carts and complex admin dashboards in favour of how Old City jewelry buyers and showroom counters actually operate:

- **Ready-Stock Transparency (No Custom Orders):** The showroom displays ready-to-buy inventory only. When a piece sells, it moves to the bottom of the feed as a greyed-out **Sold Out** card rather than offering misleading "custom order" prompts—preserving massive catalog depth as social proof while eliminating dead-stock enquiries at the counter.
- **10-Second Counter Adoption (`/admin` PWA):** Built directly into the same repository as an installable Progressive Web App. Shop staff open the home-screen icon on the counter phone, snap a photo using the rear camera, and publish—or tap **Mark Sold** at billing in one tap.
- **WhatsApp-First Acquisition Vectors:** Replaces traditional checkout flows with pre-filled `wa.me` deep links tagged with the exact item code (`MJ-104`) so buyers can instantly ask about **916 HUID purity, today's gold rate, and making charges**, or open the pinned Google Maps showroom location.
- **Zero-Cost Serverless Runtime:** Deployed statically from GitHub to Vercel/Cloudflare Pages and backed by Supabase free tiers—sub-second loads on 4G/5G mobile data with zero server bills.

---

## 🎨 Design Token Specifications

The visual interface retains the high-contrast **"Midnight Luxury"** dark palette so gold, polki, and bridal photography pop cleanly on mobile screens:

- **Background (Midnight Space):** `#12131f`
- **Primary Accent (Light Gold Text):** `#fde688`
- **Muted Trim / Borders (Deep Bronze):** `#975e29`
- **Body Content Layer (Warm Cream):** `#f7f5f0`
- **Sold Out Card State:** Desaturated imagery (`opacity-50`) + `Sold Out` badge (item-specific WhatsApp CTA removed)
- **Typography Scale:** `Cinzel` / `Playfair Display` (Headings) | `Inter` (Functional Body, Item Codes & Metadata)

---

## 📂 Directory Architecture Map

Single-repository architecture housing both the public mobile showroom and the protected `/admin` counter PWA:

```text
├── public/
│   ├── manifest.json             # PWA config for "Add to Home Screen" on shop phone
│   └── icons/                    # Home-screen launcher icons for the counter app
├── src/
│   ├── app/
│   │   ├── layout.tsx            # Master HTML wrapper, fonts, and luxury theme tokens
│   │   ├── page.tsx              # Public live showroom grid + "Available Only" toggle
│   │   └── admin/
│   │       └── page.tsx          # Protected rear-camera uploader & one-tap "Mark Sold" feed
│   ├── components/
│   │   ├── ProductCard.tsx       # Available vs. greyed-out Sold Out tile logic
│   │   ├── FilterBar.tsx         # Category pills (Bridal, Necklace, Bangles, Daily Wear)
│   │   └── FloatingConcierge.tsx # General "Ask What Just Arrived" WhatsApp & Maps bar
│   ├── lib/
│   │   ├── supabase.ts           # Supabase client initialization
│   │   ├── compressImage.ts      # Client-side WebP compression (~200KB cap before upload)
│   │   └── whatsapp.ts           # Pre-filled wa.me deep-link builders
│   └── styles/
│       └── globals.css           # Custom design tokens and utility styles
├── .env.example                  # Required public Supabase & WhatsApp environment keys
└── package.json                  # Project dependencies (Next.js/React, Supabase JS, browser-image-compression)
```

---

## ⚙️ Data Layer & Inventory Rules (Supabase)

### 1. Database Schema (`products` table)

Configure a 7-column PostgreSQL table in Supabase:

| Column | Data Type | Default / Constraint | Purpose |
| --- | --- | --- | --- |
| `id` | `uuid` | `gen_random_uuid()` (PK) | Unique record identifier |
| `code` | `text` | `unique`, `not null` | Auto-incremented showroom tag (e.g., `MJ-104`) |
| `category` | `text` | `not null` | `Bridal`, `Necklace`, `Bangles`, or `Daily Wear` |
| `image_url` | `text` | `not null` | Public WebP URL from `catalog-images` bucket |
| `status` | `text` | `'available'` | `'available'` or `'sold_out'` |
| `created_at` | `timestamptz` | `now()` | Used to sort newest arrivals first |
| `sold_at` | `timestamptz` | `nullable` | Timestamp set when marked `sold_out` |

### 2. Feed Sorting & Lifecycle Logic

- **Priority Ordering:** Public queries sort `status ASC` (`available` pinned at the top, `sold_out` pushed to the bottom) and `created_at DESC` within each group.
- **Available-Only Toggle:** Shoppers can toggle a single filter at the top of the showroom to hide `sold_out` cards immediately.
- **45-Day Sold Auto-Expiry:** Items with `sold_at` older than 30–45 days are automatically excluded from the public query so the showroom stays massive and active without turning into a stale archive.
- **Client-Side Image Compression:** All camera captures (`capture="environment"`) are compressed in-browser to **~200KB WebP** before hitting Supabase Storage, keeping 4G page loads instant and staying well inside the 1GB free storage tier.

### 3. Security & Row Level Security (RLS)

- **Auth:** Create a single shop admin account in **Supabase Auth > Users** and disable public user sign-ups.
- **Table & Bucket Policies:** Enable RLS on `products` and the `catalog-images` storage bucket:
  - `SELECT`: Public (`anon` + `authenticated`)
  - `INSERT` & `UPDATE`: Restricted strictly to `authenticated` role

---

## 🚀 Deployment & Counter Onboarding

### Step 1: Configure Environment Variables

Add the following keys to your Vercel or Cloudflare Pages project settings:

```env
NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
NEXT_PUBLIC_WHATSAPP_NUMBER=91XXXXXXXXXX
NEXT_PUBLIC_MAPS_URL=[https://maps.google.com/?q=Mohsin+Jewelers+Hyderabad](https://maps.google.com/?q=Mohsin+Jewelers+Hyderabad)
```

### Step 2: Deploy from GitHub

1. Push the repository to GitHub (`main` branch).
2. Import the repo into **Vercel** or **Cloudflare Pages** (zero-config static/hybrid deployment).
3. Verify the public showroom at `/` and the login gate at `/admin`.

### Step 3: Shop Phone & WhatsApp Business Setup

1. Open `/admin` in Chrome/Safari on the showroom phone, sign in once, and tap **Add to Home Screen** to install the Pocket Catalog PWA.
2. Convert the showroom contact number to **WhatsApp Business**, pin the store address on Google Maps, and configure Quick Replies (`/rate`, `/making`, `/location`, `/timings`).
3. Link the live showroom URL in the **Mohsin Jewelers** Instagram bio, YouTube channel description, and pinned Reel/Short comments.
