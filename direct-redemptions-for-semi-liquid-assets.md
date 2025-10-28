# Direct redemptions for semi-liquid assets

## Low instant liquidity problem

One challenge in executing leveraged strategies is the high cost of converting collateral tokens back into their underlying assets. This happens because native redemptions are often time-locked, and secondary market liquidity is typically low relative to the size of leveraged positions.

Before Gearbox it was only possible to either repay the full debt and withdrawl collateral, or iteratively deleverage withdrawing and redeeming small portions of collateral. Read more about problems of this methods [here](https://hackmd.io/@desnake/ByismSraee).

## Gearbox solution

**Benefits:**

* Save time up to **8 periods** of native redemption.
* Capital requirements are reduced by **10x**.
* Save fees equal to a **month of farming yield**.

The solution is based on unique features of Gearbox and therefore is impossible on other lending platforms:&#x20;

* **Credit Accounts**\
  Collateral and debt is held on smart accounts allowing complex interactions with DeFi protocols
* **Liquid collateral** \
  Credit accounts allow manipulating collateral, requiring overcollateralization after each transaction

## How it's done

1. The Credit Account holds an xRWA token and has an outstanding USDT debt.
2. The user starts the redemption process.
   * The Credit Account sends the xRWA token to the redemption contract.
   * In return, the Credit Account receives a _redemption receipt token_, which represents a future claim on the underlying asset.
3. The Credit Account now holds the redemption receipt token and still has the USDT debt.
4. After the Redemption Window:
   * Once the redemption window has passed, the user can finalize the redemption.
   * The Credit Account burns the redemption receipt token.
   * The Credit Account receives the underlying asset.

{% hint style="info" %}
## The Credit Account always stays overcollateralized, it's just the collateral which transfrom from xRWA into _redemption receipt token_ and eventually into liquid underlying.
{% endhint %}

## Risks & Mitigation

When assets are in a transition state (e.g., during vault token redemption to the underlying asset), they become non-transferable and therefore cannot be liquidated. In addition, these tokens typically do not earn yield during this period.

As a result, a position’s Health Factor may decrease due to:

* Vault exchange rate repricing
* Accrued borrow interest

To mitigate the risk of a position falling below the solvency threshold, it is recommended to set the reserve feed of the _phantom token_ (the token representing a future claim on redeemed assets) to a discounted value.

This discount acts as a protective buffer, ensuring that only positions with a sufficient Health Factor can enter the transition state. In practice, it prevents unhealthy positions from initiating redemptions that could lead to insolvency.

{% hint style="success" %}
For example, if a 4% reserve price discount is applied, only users with a Health Factor ≥ 1.04 will be able to initiate a full redemption of their collateral.
{% endhint %}

{% hint style="info" %}
_Health Factor = Collateral value \* LTV / Debt_\
_Positions become liquidatable if Health Factor <= 1_
{% endhint %}

**Example:**

*   mHYPER ⇒ USDC redemption

    Main phantom token price: 1 USDC

    Reserve phantom token price: 0.96 USDC

    * User holds mHYPER with position Health Factor of 1.1
      * User initiates the redemption of all mHYPER for USDC
      * User holds mHYPER ⇒ USDC phantom token with position Health Factor of 1.1
    * User holds mHYPER with position Health Factor of 1.03
      * User can initiate withdrawal only for 74% of his mHYPER
      * User holds 26% mHYPER and 74% mHYPER ⇒ USDC phantom token. Position Health Factor \~ 1.04

**Result:**

* <mark style="background-color:$success;">Conservative positions (with higher Health Factors) can redeem their full collateral size.</mark>
* <mark style="background-color:$warning;">Riskier positions must retain part of their collateral as liquid tokens, serving as a buffer that can be used for partial liquidations or deleverage if needed.</mark>

{% hint style="danger" %}
Case for careful consideration:\
\- Pool's underlying token = token1 (e.g. USDT)\
\- Phantom token's underlying token = token2 (e.g. mHYPER is withdrawn into USDC)\
\- So position in withdrawal queue may become liquidatable if USDT to USDC price rises
{% endhint %}
