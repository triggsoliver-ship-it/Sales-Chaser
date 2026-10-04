# Payments — Sales Chaser (saleschaser.co.uk)

Checkout is three things and no more: one config object at the top of
`checkout.js`, one `data-checkout` attribute on the button in `index.html`, and
Stripe. No dependencies, no build step, no server, no API key.

## Status — checkout switched off, new link needed

**The price changed on 4 October 2026: £50 → £25 per qualified lead.** The owner
chose it after a check of competitor pricing (see "Price check" at the bottom).

The Payment Link in use until then charges £50, so it was removed from
`checkout.js` in the same commit. A page that says £25 must never hand off to a
checkout that takes £50. With the key blank the buy button stays the `mailto:`
it ships as, which `enquire.js` opens as the enquiry form — nothing on the page
is dead, but nobody can buy by card until a new link exists.

To switch checkout back on:

1. In Stripe, create a new Payment Link: **£25**, GBP, one-off, **quantity
   adjustable**, no Stripe Tax.
2. Paste it into `per_lead` in `checkout.js`.
3. Click it through on the live site and check Stripe's page shows £25 before
   telling anyone it is live.

The old link, for reference only — do not paste it back, and deactivate it in
Stripe once nothing depends on it: `https://buy.stripe.com/5kQ4gyaCh3tld9Nb2QeIw0o`
(£50).

## Keys

| Key | Where it appears | Must charge | Payment Link |
|---|---|---|---|
| `per_lead` | `index.html` → Pricing → **Pay Per Qualified Lead** card, primary button | **£25 per qualified lead**, GBP, **quantity adjustable at checkout** | not set — see Status above |

The link must have adjustable quantity switched on in Stripe, so a customer can
buy several leads in one go. The button therefore says "Buy leads — £25 each"
rather than anything implying a single purchase. If quantity is ever switched
off in Stripe, change the label to match.

Keelson Holdings Ltd is **not VAT registered**. £25 is the whole price of one
lead — nothing is added at checkout, and no VAT is charged or implied.

**Managed Campaign** and **High Volume** are custom priced and are deliberately
not wired. Their buttons are `mailto:` links and must stay that way.

## Button labels

The price is in the label on purpose. If the wrong link is ever pasted in, the
Stripe page shows a different number from the button that got you there, and the
mistake is obvious before anyone is charged.

| Key | Ships as (mailto) | Reads as once upgraded |
|---|---|---|
| `per_lead` | `Enquire to buy leads — £25 each` | `Buy leads — £25 each` |

## The fallback contract

The buy button is served with its existing `mailto:` link already in the `href`.
`checkout.js` replaces that href **only** when the configured value matches:

    /^https:\/\/(?:buy|checkout)\.stripe\.com\/[^\s"']+$/

If it does not match, the button is left exactly as it shipped — same href, same
label — and the visitor gets the same contact behaviour the site had before
checkout existed. The site is therefore safe with no configuration and safe with
bad configuration. It is also safe with JavaScript disabled: the button is still
a working contact link.

These all fall through, and were tested:

| Configured value | Result |
|---|---|
| `""` | falls through — empty |
| `"TODO"` | falls through — placeholder |
| `http://buy.stripe.com/5kQ4gyaCh3tld9Nb2QeIw0o` | falls through — not https |
| `https://buy.stripe.com` | falls through — no path |
| `https://buy.stripe.com.evil.example/5kQ4gyaCh3tld9Nb2QeIw0o` | falls through — lookalike host |

Only `buy.stripe.com` and `checkout.stripe.com`, over https, with a non-empty
path, are accepted.

To check the live site, open the console and run `CHECKOUT.isLive(value)`, or
inspect `CHECKOUT.links`.

## Changing a price

1. Change it in Stripe. A Payment Link's price lives in Stripe, never here.
2. If the link itself changed, update the URL in `checkout.js`.
3. Update the number on the card **and** both button labels in `index.html`, and
   the row in this file. All three must agree with Stripe.

## Rules

- Never commit a Stripe key. Payment Link URLs are public and safe; `sk_`, `rk_`
  and webhook secrets are not, and none of them are needed for this.
- No dependencies and no build step. `checkout.js` is plain ES5 served static.
- The free-demo CTAs — nav, hero and closing section — are lead magnets. They
  convert better than a cold buy button. Do not turn them into checkout buttons.
- This repo has no `vercel.json`, so there is no CSP and no Permissions-Policy to
  fix. If one is ever added it must not disable the `payment` permission, and it
  must allow `buy.stripe.com` and `checkout.stripe.com` in `form-action` and
  `connect-src`.

## Price check — 4 October 2026

Published prices found on 4 October 2026. They back the "How that compares"
table in the pricing section and the move to £25. Prices move; re-check before
quoting any of them. Only WillPower and Retell were read on the provider's own
site — the rest come from listings and comparison pages.

| Type | Provider | Published price |
|---|---|---|
| Done-for-you AI lead calling (UK) | WillPower LeadGen, Speed to Lead | £1,000 setup + £300 a month + £2 per lead called |
| Done-for-you AI lead qualification (UK) | HyperLeads | from £450 a month |
| Dialler software | CloudTalk, JustCall, Aircall | from $19, $29 and $30 per user a month; seat minimums on the last two |
| Dialler software | PhoneBurner | from $140 per user a month |
| DIY AI calling platform | Retell AI | roughly $0.07 to $0.15 per minute all in |
| DIY AI calling platform | Bland AI | $299 to $499 a month plus per-minute charges |
| AI sales tools | AiSDR | $250 to $2,500 a month |
| AI sales tools | 11x | from $3,750 a month |
| Pay-per-lead agencies | typical range | $50 to $300 per lead |

Sales Chaser has no monthly fee, so it is the cheapest of these per month. No
other provider found sells AI qualification of a client's own leads on a
pay-per-qualified-lead basis, so there is no like-for-like per-lead price.
