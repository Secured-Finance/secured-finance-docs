# November 2026 Security Update

On 5 November 2026, Fixed-Rate Lending trading, deposits and withdrawals were temporarily paused as a precaution after an order-book pricing issue was identified. Updated contracts and apps were deployed on 6 November, and the engineering team subsequently confirmed unpausing.

### Strengthened circuit-breaker controls

The update strengthens order-price safeguards on Ethereum Mainnet, Arbitrum One and Filecoin:

* Lending and borrowing controls use a common reference derived from previous reliable block prices.
* Trades within the current block do not change that reference during the block.
* Active-market limit orders are checked against the applicable circuit-breaker bounds and existing order-price range.

### Using the updated markets

Active-market limit orders must be within the permitted price range. Integrators should check the updated contract ABI and LendingMarketReader deployment records.

This update describes the deployed safeguards; it is not an independent audit or a guarantee against all market risks.

See [Contract Upgrade History](https://docs.secured.finance/fixed-rate-lending/contracts-and-security/contract-upgrade-history) for code references and chain-specific execution transactions.

Last updated: 6 November 2026 (UTC).
