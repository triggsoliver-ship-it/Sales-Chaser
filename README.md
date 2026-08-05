# Sales Chaser

AI lead-qualification service — a Ship It Studio company.

We call your **opted-in** leads within 60 seconds, qualify them to your script, and book the hot ones straight onto your sales team's calendar. Pay per qualified lead.

- **Live site:** saleschaser.co.uk
- **Model:** opted-in / warm leads only (UK PECR compliant) — never cold AI dialling
- **Static site:** `index.html` (single file), deployed on Vercel
- **Pricing:** from £50/qualified lead · Managed Campaign custom · High Volume custom
- **Contact / CTA:** all calls-to-action are `mailto:info@shipitstudio.co.uk`

## Notes

- The call transcript in the hero is an **illustrative demo** — "Bright Spark Solar" and the Mark/Sarah exchange are a worked example, not a real customer.
- Headline stats are marked `*industry estimates, sources on request`.
- `googlea33b0815e7fc268d.html` is byte-identical to the one in the callcatcher repo. Google issues a distinct token per property, so only one of the two domains can actually be verified by it — worth confirming in Search Console.
- Vercel Web Analytics loads from `https://cdn.vercel-insights.com/v1/script.js`. The callcatcher site uses the current first-party path `/_vercel/insights/script.js`, which is ad-blocker resistant and already resolves on this domain — worth switching for accurate numbers.
- `sitemap.xml` `<lastmod>` is 2026-07-21, which matches the real last content change. Keep it in step with actual `index.html` edits rather than bumping it on every deploy.
