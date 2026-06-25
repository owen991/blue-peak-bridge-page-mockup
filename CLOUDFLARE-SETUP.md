# Cloudflare Pages setup — bridge page (for Teagan, ~10 min, one time)

This repo holds the SC foreclosure **bridge page** (`index.html`) — the page leads land on after they say
"yes" to the guide. We're moving it from the GHL funnel to **Cloudflare Pages** (faster, link-preview cards,
scales to more guides). Owen owns the page + pushes updates; this one-time Cloudflare setup needs your account.

> Note: we're still in test phase, so it's fine if `go.bluepeak-ventures.com` briefly goes down during the
> domain switch — no live traffic depends on it yet.

## Step 1 — Create the Pages project (deploys to a test URL, no domain change)
1. Cloudflare dashboard → **Workers & Pages → Create → Pages → Connect to Git**.
2. Authorize Cloudflare's GitHub app for **`owen991/blue-peak-bridge-page-mockup`** (it's Owen's repo) and select it.
3. Build settings: **Framework preset = None**, **Build command = (leave blank)**, **Build output directory = `/`** (root).
4. **Save and Deploy.** It builds in ~30s and gives a `https://<project>.pages.dev` URL.
5. Open that URL and sanity-check: video loads, calendar loads, **book a test appointment** and confirm it
   comes through (it uses the same live GHL calendar `OZGuFcFjKOGauHzP02lM`, so bookings flow exactly as today).

→ At this point nothing about the live `go.` domain has changed. The Cloudflare page just lives at `*.pages.dev`.

## Step 2 — Point the domain at it (the actual cutover)
1. In the Pages project → **Custom domains → Set up a custom domain → `go.bluepeak-ventures.com`**.
2. Because `bluepeak-ventures.com` is already on Cloudflare, it auto-creates the DNS record and provisions SSL.
   Wait until the custom domain shows **Active** + **SSL Active** (a few minutes, not instant).
3. Load `https://go.bluepeak-ventures.com`, book one more test, confirm it lands.

This re-points `go.` from the GHL funnel host to the Cloudflare page.

## Rollback (if needed)
Remove the custom domain from the Pages project (or point `go.` back to the GHL funnel host). The page returns
to GHL within the DNS TTL. Keep the old GHL funnel **published** until we've soaked the Cloudflare page.

## After cutover
- Updates: Owen pushes to this repo → Cloudflare auto-redeploys. No further Cloudflare steps needed.
- TODO (Owen): add `og-foreclosure.png` (1200×630) for the texted-link preview card — tags are in place, image pending.
