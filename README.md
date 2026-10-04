# Sales Chaser

AI lead-qualification service — a Ship It Studio company.

We call your **opted-in** leads within 60 seconds, qualify them to your script, and book the hot ones straight onto your sales team's calendar. Pay per qualified lead.

- **Live site:** saleschaser.co.uk
- **Model:** opted-in / warm leads only (UK PECR compliant) — never cold AI dialling
- **Static site:** `index.html`, `privacy.html` and `checkout.js`, deployed on Vercel
- **Pricing:** £25/qualified lead, no monthly fee · Managed Campaign custom · High Volume custom (changed from £50 on 4 October 2026 — see PAYMENTS.md)
- **Contact / CTA:** the Pay Per Qualified Lead card has a Stripe buy button at £25 per lead; every other call-to-action is `mailto:info@shipitstudio.co.uk`, opened as a real enquiry form by `enquire.js`

## Checkout

The Pay Per Qualified Lead card is priced at £25 per lead. Its buy button takes
a Stripe Payment Link (quantity adjustable at checkout) from one config object
at the top of `checkout.js`. The button ships with its existing `mailto:` href
and is only upgraded when the configured value is a real Stripe Payment Link, so
the site still works with no configuration, bad configuration or JavaScript off.

**The link itself did not change on 4 October 2026.** The price behind it was
changed in Stripe from £50 to £25, so the same URL now charges £25. Managed
Campaign and High Volume are custom priced and are not wired. See `PAYMENTS.md`.

## Notes

- The call transcript in the hero is an **illustrative demo** — "Bright Spark Solar" and the Mark/Sarah exchange are a worked example, not a real customer.
- Headline stats are marked `*industry estimates, sources on request`.
- `googlea33b0815e7fc268d.html` is byte-identical to the one in the callcatcher repo. Google issues a distinct token per property, so only one of the two domains can actually be verified by it — worth confirming in Search Console.
- Vercel Web Analytics loads from `https://cdn.vercel-insights.com/v1/script.js`. The callcatcher site uses the current first-party path `/_vercel/insights/script.js`, which is ad-blocker resistant and already resolves on this domain — worth switching for accurate numbers.
- `sitemap.xml` `<lastmod>` for the home page is 2026-10-04, the day the price changed, which matches the real last content change. Keep it in step with actual `index.html` edits rather than bumping it on every deploy.
- The "How that compares" table in the pricing section describes how each type of rival charges, checked on 4 October 2026. The figures behind it are listed in `PAYMENTS.md`. Re-check them before relying on the table for long.
