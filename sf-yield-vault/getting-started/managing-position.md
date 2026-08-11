---
description: What to monitor after depositing, and when to act
---

# 📈 Manage your position

A vault position needs no active management — you don't select strategies, rebalance, or track maturities. Managing a position means **monitoring its value and deciding when to add or withdraw**.

## The three numbers that matter

| Metric | What it tells you |
| --- | --- |
| **Share balance** | Your vault shares. Constant unless you deposit or withdraw |
| **Value per share** | How much base asset each share represents. Rises with yield, falls with losses — this is the number to watch |
| **Estimated value** | Share balance × value per share: your position in base-asset terms |

Yield never arrives as separate tokens — it shows up entirely through the value per share, which also means it compounds automatically.

{% hint style="info" %}
**Your share balance not changing is normal.** Growth (or loss) appears in the value per share. Compare your estimated value against what you deposited to see your actual performance — the app also shows vault APY over 7 days, 30 days, and since inception.
{% endhint %}

## Adding to your position

Deposit more into the same vault at any time. New shares are minted at the current value per share; your existing shares are unaffected.

## Reducing or exiting

Withdraw any portion by redeeming shares — see [Withdraw assets](withdrawing-assets.md). Common reasons to reduce: cutting exposure, reallocating capital, or the strategy's risk no longer fitting your preference. Vaults are designed for medium- to long-term participation rather than frequent in-and-out trading.

{% hint style="warning" %}
**Value can go down.** A negative period — such as a strategy loss or adverse market move — reduces the value per share and your estimated value, even if you take no action. See [Risks](../faqs.md#risks).
{% endhint %}

## Related

* [Platform guide](platform-guide.md) — every tab and metric in the interface
* [Vault System Overview](../core-mechanics/vault-system-overview.md) — the accounting behind the numbers
* [Available Vaults and Strategies](../core-mechanics/available-vaults-and-strategies/README.md) — what your vault invests in
