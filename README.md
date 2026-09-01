# Sales Chaser

AI lead-qualification service — a Ship It Studio company.

We call your **opted-in** leads within 60 seconds, qualify them to your script, and book the hot ones straight onto your sales team's calendar. Pay per qualified lead.

- **Live site:** saleschaser.co.uk
- **Model:** opted-in / warm leads only (UK PECR compliant) — never cold AI dialling
- **Static site:** `index.html`, `privacy.html` and `checkout.js`, deployed on Vercel
- **Pricing:** £50/qualified lead · Managed Campaign custom · High Volume custom
- **Contact / CTA:** the Pay Per Qualified Lead card has a Stripe buy button; every other call-to-action is `mailto:info@shipitstudio.co.uk`

## Checkout

The Pay Per Qualified Lead card has a Stripe buy button at £50 per lead, with
quantity adjustable at checkout. The Payment Link URL lives in one config object
at the top of `checkout.js`. The button ships with its existing `mailto:` href
and is only upgraded when the configured value is a real Stripe Payment Link, so
the site still works with no configuration, bad configuration or JavaScript off.
Managed Campaign and High Volume are custom priced and are not wired.
See `PAYMENTS.md`.

## Notes

- The call transcript in the hero is an **illustrative demo** — "Bright Spark Solar" and the Mark/Sarah exchange are a worked example, not a real customer.
- Headline stats are marked `*industry estimates, sources on request`.
- `googlea33b0815e7fc268d.html` is byte-identical to the one in the callcatcher repo. Google issues a distinct token per property, so only one of the two domains can actually be verified by it — worth confirming in Search Console.
- Vercel Web Analytics loads from `https://cdn.vercel-insights.com/v1/script.js`. The callcatcher site uses the current first-party path `/_vercel/insights/script.js`, which is ad-blocker resistant and already resolves on this domain — worth switching for accurate numbers.
- `sitemap.xml` `<lastmod>` is 2026-09-01, the day checkout was added, which matches the real last content change. Keep it in step with actual `index.html` edits rather than bumping it on every deploy.
