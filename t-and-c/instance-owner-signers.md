# Instance Owner signers

***

### 1) Purpose & Scope

These Terms & Conditions define the minimum due‑diligence and neutral‑gatekeeping standards for IO signers when **adding, configuring, or allowing** price feeds in the **Price Feed Store (PFS)** on any supported EVM chain. The sole goal is to ensure that, **at the moment of signing**, every configured feed **returns an adequate market price for the intended token, normalized to 8 decimals**, and satisfies staleness / quality constraints.

> Scope explicitly excludes any market‑risk, business, or curation decisions. IO signers act only as neutral technical gatekeepers.

***

### 2) Authority, Membership & Neutrality (summary)

* **Authority (PFS):** IO may add/remove feeds; set staleness period; attach/detach feeds to tokens; and run feed configuration calls required by integrated providers.
* **Neutrality:** IO remains **business-neutral**. Decisions must be based **only on objective technical criteria** below. All valid, safe requests should be processed in a reasonable timeframe.
* **Non‑interference with markets:** PFS changes **do not alter behavior of existing Markets by themselves** and **are not auto‑applied** to them.

***

### 3) Definitions & Expectations

* **Price Feed Store (PFS):** Chain‑specific registry of tokens and feeds. A token can be used as collateral only after its token entry and at least one allowed feed are present.
* **8‑decimal normalization:** All effective Gearbox price feeds **must return USD‑denominated prices with 8 decimals** (`1e8` scale). Signers should verify output scale when checking a feed.
* **Staleness Period:** Maximum allowed time since last update before a feed is considered stale and reverts/invalidates.
* **Adequate market price:** A price reasonably close to reputable sources at the time of signing.

***

### 4) Pre‑Signing Due‑Diligence (hard requirements)

**Signers must complete all checks below before approving the transaction.** If any check fails, **do not sign.**

#### 4.1 Contract & Deployment

1. **Feed contract is verified** on a reputable explorer (Etherscan/chain explorer) and **matches the intended implementation** (e.g., AggregatorV3‑compatible external, Pyth/Redstone wrapper, ERC4626 feed, Pendle PT TWAP, etc.).

#### 4.2 Price Output & Decimals

1. **Price sanity:** Read the feed (via explorer read panel, provider dashboard, or PFS UI). The value must be **within a reasonable range** of one or more of:
   1. **CoinGecko** (or equivalent public index),
   2. **Trusted DEX/aggregators** (Uniswap/Curve/Balancer; 1inch/Cow/Odos),
   3. **Designated platforms** when public indexes are unavailable (e.g., **Pendle markets** for PTs; **Pyth Insights**; **Redstone App**; protocol UIs for ERC4626 vault exchange rate).
2. **Decimals:** Confirm that the effective price value is **normalized to 8 decimals**.

#### 4.3 Staleness

1. **Staleness period** must be reasonable for the source and chain:
   1. **Pull‑type feeds (e.g., Pyth/Redstone pull):** _recommended_ `240s` (4 min) unless documented otherwise.
   2. **External Aggregator feeds (push/heartbeat):** heartbeat **+ 15 min** (slow chains) or **+ 2 min** (fast chains).&#x20;

#### 4.4 Asset‑Specific Parameters (when applicable)

1. **Stablecoin‑to‑USD feeds:** The observed price must be **bounded from above at 1.04**. Any stablecoin feed reporting a price above this bound should be treated as invalid and must not be signed.
2. **LST/LRT‑to‑ETH or to BTC feeds:** The observed ratio must be **bounded from above at 1.04**. If the ratio exceeds this bound, the feed is considered invalid and the transaction must not be signed.

***

### 5) Refusal & Escalation Policy

If **any** requirement in fails or is inconclusive, **decline to sign**. Examples:

* Contract not verified / ownership unclear;
* Output not 8‑decimals normalized;
* Price materially diverges from reputable venues;
* Staleness period unreasonable for the source/chain;
* Source‑specific parameters missing/incorrect.

***
