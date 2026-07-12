---
description: Yield curves and market data — no wallet required
---

# Markets

The [**Markets**](https://app.secured.finance/dashboard/) tab is the protocol's data dashboard. It works without connecting a wallet.

<!-- screenshot: markets-dashboard -->

## What you'll find

* **Yield curves** — fixed rates across all quarterly maturities per currency. Select a currency to view its curve; compare currencies to spot relative-value opportunities.
* **Key metrics** — total value locked, trading volume (24h/7d/30d), number of traded assets, and active users.
* **Chain status** — health of each supported network.

## Reading the yield curve

* **Upward-sloping (steep)** — the market demands a premium for longer terms; lenders may find better rates at longer maturities.
* **Flat or inverted** — near-term rates equal or exceed long-term rates, often signaling expectations of falling rates or near-term stress.
* Click any market to jump straight into the [Trading](trading.md) interface for that currency and maturity.

{% hint style="info" %}
During the 7-day pre-open window before a new market launches, the curve shows the **estimated opening APR** derived from the [Itayose](../../advanced-topics/itayose.md) order book.
{% endhint %}

## Troubleshooting

* **Data not loading** — refresh; check your connection; try another browser.
* **Curve not displaying** — ensure JavaScript is enabled and no extension is blocking charts.
