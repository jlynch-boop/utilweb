# netfee.io

Static site for [netfee.io](https://netfee.io) — honest payment-processor fee calculators. No framework, no build step, pure HTML + a shared CSS file.

Operated by Robot Arms LLC (Colorado). Not affiliated with Stripe, Square, PayPal, or Shopify.

## Layout

```
site/
├── index.html                      # Homepage
├── stripe-fee-calculator.html      # Stripe calculator
├── square-fee-calculator.html      # Square calculator
├── paypal-fee-calculator.html      # PayPal calculator
├── compare.html                    # Head-to-head comparison
├── privacy.html                    # Privacy policy
├── terms.html                      # Terms + affiliate disclosure
├── contact.html                    # Contact page
├── styles.css                      # Shared design system
├── .gitignore
└── README.md
```

## Local preview

No build step. Serve the directory as static files:

```bash
python3 -m http.server 8787
# then open http://localhost:8787/
```

Or use any static server: `npx serve`, `caddy file-server`, etc.

## Deploy — Cloudflare Pages

1. Push this repo to GitHub (e.g., `github.com/netfee/site` or similar)
2. Cloudflare Pages → **Create a project** → connect the GitHub repo
3. Build settings: **no build command**, output directory `/` (root)
4. Deploy

Pages gives you a `*.pages.dev` URL immediately. To attach `netfee.io`:

1. Cloudflare dashboard → Pages project → **Custom domains** → add `netfee.io` and `www.netfee.io`
2. Porkbun → `netfee.io` → **Authoritative Nameservers** → switch to Cloudflare's (e.g., `kira.ns.cloudflare.com` + `rick.ns.cloudflare.com`)
3. Cloudflare will provision SSL automatically within ~5 min
4. Ensure a CNAME in Cloudflare DNS: `@` and `www` pointing to the `*.pages.dev` domain (Pages often sets this automatically when you add a custom domain)

## Design system

All visual styling lives in `styles.css`. Changes there apply to every page. Page-specific styling is limited to `<script>` blocks (calculator logic) — each page is self-contained otherwise.

CSS variables in `:root` control the palette, fonts, and radii. Adjust once, propagate everywhere.

## Monetization scaffolding

Each calculator page and the homepage have three commented-out AdSense slot placeholders and an affiliate CTA block with placeholder tracked URLs:

- **AdSense:** `<!-- AdSense in-article unit -->` blocks — uncomment and paste publisher ID + slot IDs after approval
- **Affiliate:** `PLACEHOLDER-SHOPIFY`, `PLACEHOLDER-SQUARE`, `PLACEHOLDER-PAYPAL` tracked-URL placeholders — swap post-approval

Activation steps are tracked in the project wiki at `../Util_Web/wiki/concepts/Affiliate and AdSense Setup.md`.

## Rate currency

Rates on every calculator page are tagged "current as of April 2026". When processors update pricing, update the corresponding page's rate tables, `RATES` JS constants, and the "Last verified" dates.
