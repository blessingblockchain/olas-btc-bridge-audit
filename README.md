# Olas BTC Bridge — Security Audit Findings

Security audit of the [Near-One/btc-bridge](https://github.com/Near-One/btc-bridge) (Satoshi Bridge) smart contracts.

## Findings

| # | Title | Severity | PoC |
|---|-------|----------|-----|
| 6 | [`is_refund_required()` returns `false` for `PromiseResult::Failed` — user BTC permanently absorbed](./FINDING_6_REPORT.md) | High | Yes |

## Scope

- `contracts/satoshi-bridge/src/btc_light_client/deposit.rs`
- `contracts/satoshi-bridge/src/nbtc/mint.rs`
- NEAR cross-contract call (XCC) callback error handling
