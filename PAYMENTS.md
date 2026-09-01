# Payments — Sales Chaser (saleschaser.co.uk)

Checkout is three things and no more: one config object at the top of
`checkout.js`, one `data-checkout` attribute on the button in `index.html`, and
Stripe. No dependencies, no build step, no server, no API key.

## Keys

| Key | Where it appears | Must charge | Payment Link |
|---|---|---|---|
| `per_lead` | `index.html` → Pricing → **Pay Per Qualified Lead** card, primary button | **£50 per qualified lead**, GBP, **quantity adjustable at checkout** | `https://buy.stripe.com/5kQ4gyaCh3tld9Nb2QeIw0o` |

The link has adjustable quantity switched on in Stripe, so a customer can buy
several leads in one go. The button therefore says "Buy leads — £50 each" rather
than anything implying a single purchase. If quantity is ever switched off in
Stripe, change the label to match.

Keelson Holdings Ltd is **not VAT registered**. £50 is the whole price of one
lead — nothing is added at checkout, and no VAT is charged or implied.

**Managed Campaign** and **High Volume** are custom priced and are deliberately
not wired. Their buttons are `mailto:` links and must stay that way.

## Button labels

The price is in the label on purpose. If the wrong link is ever pasted in, the
Stripe page shows a different number from the button that got you there, and the
mistake is obvious before anyone is charged.

| Key | Ships as (mailto) | Reads as once upgraded |
|---|---|---|
| `per_lead` | `Enquire to buy leads — £50 each` | `Buy leads — £50 each` |

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
