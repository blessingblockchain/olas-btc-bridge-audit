# Olas BTC Bridge — Security Audit Findings

Security audit of the [Near-One/btc-bridge](https://github.com/Near-One/btc-bridge) (Satoshi Bridge) smart contracts.

## Findings

| # | Title | Severity | PoC |
|---|-------|----------|-----|
| 4 | [Insufficient gas in `verify_withdraw_burn_callback` — permanent fund loss on cancel-withdraw](./FINDING_4_REPORT.md) | High | Yes |

## Scope

- `contracts/satoshi-bridge/src/nbtc/burn.rs` — gas allocation for withdraw burn callback
- `contracts/satoshi-bridge/src/token_transfer.rs` — child promise gas requirements
- `contracts/satoshi-bridge/src/rbf/cancel_withdraw.rs` — cancel-withdraw refund logic
- NEAR cross-contract call (XCC) gas accounting and promise chain failures

## Test Infrastructure

All PoCs run in the project's own `near-workspaces` sandbox with real deployed contracts (no mocks). Tests are in `contracts/satoshi-bridge/tests/test_satoshi_bridge.rs`.

### Run the PoC

```bash
# Symlink to avoid spaces in path
ln -sf "/path/to/btc-bridge" /tmp/btc-bridge

cd /tmp/btc-bridge
CARGO_TARGET_DIR=/tmp/btc-bridge-target \
  cargo test --features "bitcoin" \
    --manifest-path ./contracts/satoshi-bridge/Cargo.toml \
    -- test_finding_4 --nocapture
```
