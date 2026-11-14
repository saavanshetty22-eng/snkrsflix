# SNKRSFLIX — Wear The Flex

A single-page sneaker storefront with a WhatsApp-based checkout. No build step, no backend: the whole site is one `index.html` file.

## Features

- Cinematic entry page with the brand logo and display pods
- Light, minimal storefront with a centred logo header
- Menu (☰) with **Men's Shoes**, **Women's Shoes** and **Accessories**, each with brands and types
- Search, bag and WhatsApp checkout in the header
- Grid / list view toggle (grid by default, 2 columns on mobile)
- Mobile bottom bar: Home, Shop, Category
- **WhatsApp Inquiry** button on every product, with a product-specific link
- Order message sent to WhatsApp includes each product's name, size, quantity, price and link
- Hidden owner portal to add, edit and delete products and change the WhatsApp number

## Files

```
├── index.html   # the entire website (HTML, CSS, JS and images)
└── README.md
```

## Run locally

Open `index.html` in any browser. Nothing to install.

## Deploy

### GitHub Pages
1. Create a new repository and upload `index.html` and `README.md`.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**, select `main` and `/ (root)`, then **Save**.
4. After a minute your site is live at `https://<your-username>.github.io/<repo-name>/`.

### Netlify / Cloudflare Pages / Vercel
Drag and drop `index.html` (or connect this repository). No build command is needed.

### Custom domain
Buy a domain, then add it in your host's **Custom domain** settings and follow the DNS steps shown.

## Configuration

All settings are near the top of the `<script>` section in `index.html`:

| What | Where |
|---|---|
| WhatsApp order number | `let WA='...'` (country code, no `+`, e.g. `918169159136`) |
| Owner portal PIN | `const PIN='...'` |
| Products, prices, sizes | the `P=[ ... ]` array |
| Menu brands / types / categories | `BR`, `TYPES`, `CATS` |

Each product looks like:

```js
{id:1, n:'Product name', b:'Air Jordan', g:'m', t:'High Top', p:3999, r:5999, i:'<image>'}
```

`g` is the section (`m` men, `w` women, `u` unisex, `a` accessory), `p` is the selling price and `r` is the strike-through MRP. Accessories use `c` (category) instead of `t`.

## Owner portal

Open your site address with `#admin-vault` at the end (for example `https://your-site/#admin-vault`), or press **Ctrl + Shift + A** on a computer, then enter the PIN.

From there you can add products through a 4-step form (Basics → Pricing → Photo → Sizes), edit or delete products, and change the WhatsApp number.

**Important**
- Portal changes are saved in the owner's browser only (`localStorage`). Other visitors will not see them. To change what everyone sees, edit `index.html` and redeploy.
- The PIN is stored in the page code, so treat it as a light lock, not real security. **Change the default PIN before going live.**
- Photos uploaded in the portal are also stored only in that browser. For the live site, add images to the `P` array in `index.html`.

## Product links

Every product has a shareable link in the form `https://your-site/#p<id>` (for example `#p3`). Opening it shows that product directly. These links are included in WhatsApp inquiries and order messages.

## Notes

- WhatsApp links cannot attach images automatically, so messages include the product link instead.
- Product photos are embedded in the file as base64, which keeps the site to one file but makes `index.html` large. Compress new photos before adding them.

## Tech

HTML, Tailwind CSS (CDN), vanilla JavaScript, Google Fonts (Syne, Space Grotesk).

## License

All rights reserved © 2026 SNKRSFLIX. Add a license here if you want others to reuse the code.
