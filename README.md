# StockHours landing page (nourtrades.com)

A static sales page for the StockHours Signals Chat, with the Vanquish Trader (code NOUR) offer and the free Discord as fallbacks. Checkout runs inside the page through Whop's embedded checkout. There's no build step.

## What changed from the current nourtrades.com

| Problem on the current site | What this page does instead |
| --- | --- |
| Phone first screen is the logo and a TradingView ticker of unrelated prices; no button in view | The headline, the 46-second video and the Join button all fit on the first screen of an iPhone 13 / Pixel 7 |
| Video autoplays muted behind a "Your Video Is Playing, Click To Unmute" box (Vidalytics) | Self-hosted video with a cover frame; tapping plays it with sound. It loads only on tap |
| 5.6 MB page, 220 images, TradingView + Vidalytics + Whop + Stripe + hCaptcha all loaded at once | About 1.5 MB on load; Whop/Stripe load only when someone touches a checkout button |
| Only 3 bullet points describe the product | "This is what a signal looks like" (Nour's real Discord posts) and "Your day inside StockHours" (from the video: pre-market voice, Maki on SPY, option flow and news, 8pm ET lessons) |
| 200 screenshots with no amounts, names or dates | Ticker of real member wins; Mohammed S.'s $7,100 posted-wins statement; 24 captioned receipts; 12 testimonials |
| No Vanquish offer: someone who won't pay $249 can only leave | Vanquish "Trade the alerts on someone else's money" section with the $300K+ claim, 4 payout cards and the NOUR code |
| No FAQ or objection handling | 9-question FAQ, starting with "Is it worth $249 a month?" and "Is this for beginners?" |
| No sticky button on phones; on phones the plan picker comes after the description | Sticky price + Join bar; the plan builder comes before the comparison table |

## Page order

1. Proof bar (★ 4.9, 729 reviews)
2. Hero: headline, video, Join button, price
3. Ticker of member wins
4. What a signal looks like (Nour's posts)
5. Your day inside StockHours (timeline)
6. One member, 23 days, $7,100 (statement)
7. Receipts wall + testimonials
8. The youngest kid on Wall Street (photos)
9. Same market, different seat (on your own vs StockHours)
10. Three steps
11. Plan builder + comparison table (`#join`), opening Whop checkout in a dialog
12. Vanquish Trader / code NOUR (`#funded`)
13. Free Discord
14. FAQ
15. Close + P.S.
16. Footer with the full legal disclosure from the current site

## Tracking

Uses the same Meta Pixel (`881783226132391`) and Google Ads tag (`AW-226885992`) as the current site.

| Moment | Meta | Google |
| --- | --- | --- |
| Page load | `PageView` | page view |
| Plans section scrolled into view | `ViewContent` | `view_item_list` |
| Video played | `VideoPlay` (custom) | `video_start` |
| Checkout opened (paid plan) | `InitiateCheckout` (value, USD) | `begin_checkout` |
| Checkout opened (free Discord) | `Lead` | `generate_lead` |
| Purchase completed (Whop `onComplete`) | `Purchase` (value, USD) | `purchase` |
| Free Discord claimed | `CompleteRegistration` | `sign_up` |
| Vanquish button | `VanquishClick` (custom) | `vanquish_click` |
| NOUR code copied | `CopyCode` (custom) | — |

To count purchases as Google Ads conversions, add a `send_to: "AW-226885992/<label>"` to the `purchase` event in `assets/app.js` using the conversion label from Google Ads.

## Files

- `index.html` — the page
- `thanks.html` — where Whop sends buyers after checkout
- `assets/styles.css` — styles
- `assets/app.js` — video, receipts, lightbox, plan builder, copy code, sticky bar, tracking
- `assets/checkout.js` — Whop embedded checkout (plan IDs live here)
- `assets/img/` — screenshots, photos, payout cards, signals, logo
- `assets/video/vsl.mp4` — 1080p welcome video (8 MB)
- `vercel.json` — cache headers

## Plans

| Plan | Price | Whop plan |
| --- | --- | --- |
| Signals Chat · Monthly | $249/mo | `plan_mNqOeTtQdUwdI` |
| Signals Chat · 3 months | $499.99 | `plan_rJGyBGGeKU3xL` |
| VIP Bundle · Monthly | $275/mo | `plan_gSHcTOO8Tepwk` |
| VIP Bundle · 3 months | $549.99 | `plan_ZRJSPKXw7ttxY` |
| Free Discord | $0 | `plan_WafKE7MWvAvTm` |

## Deploy

1. Import this repo in Vercel (framework preset **Other**, no build command, output = repo root).
2. Check a test purchase on the preview URL, then point nourtrades.com at it.

Preview locally with `python3 -m http.server 8000`.
