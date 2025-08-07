# Direct withdrawals

## Low instant liquidity problem

Leveraged looping has become one of the main usecases of lending protocols. In this case collateral and debt token are highly correlated and the end goal is usually earning yield on token which is being borrowed.

One of the problems that arise during execution of such strategies is cost of withdrawals from collateral token into underlying, as native redemption is usually timelocked and secondary liquidity is low compared to typical leveraged position size.

## Gearbox solution

<table><thead><tr><th>Cost</th><th width="219.15234375">Gearbox direct withdrawal</th><th width="177.99609375">Full debt repayment</th><th width="190.3671875">Iterative unwinding</th></tr></thead><tbody><tr><td>Total redemption time, days</td><td>7-14 days</td><td>7-14 days</td><td>28-56 <br>(42-84)</td></tr><tr><td>Capital requirements</td><td>0</td><td>32k WETH <br>(45k WETH)</td><td>0</td></tr><tr><td>Fees (farming time equivalent, days)</td><td>0</td><td>20 (0)</td><td>20 (0)</td></tr></tbody></table>

**Note:** numbers in parentheses represent the case where instant liquidity is not used, therefore no fee for it is paid.

The solution is based on unique features of Gearbox and therefore is impossible on other lending platforms:&#x20;

* **Liquid collateral** \
  Swap collaterals inside credit account without unwinding position
* **Credit Account Abstraction**\
  Collateral and debt is held on smart accounts allowing complex interactions with DeFi protocols

#### Conceptual explanation:

The core idea of solution is tokenizing User's position in withdrawal queue:

* User initiated redemption of 1k rstETH through Gearbox adapter and sent rstETH to withdrawal contract
* Gearbox adapter minted 1k Withdrawal Phantom Tokens (WPT) to user, representing user's claim for withdrawn wstETH
* When wstETH is unstaked and withdrawn by user, he burns Withdrawal Phantom Tokens and receives wstETH

#### Risks and curator's job:

* Withdrawal Phantom Token (WPT) is a new unique type of collateral which has its own risk parameters that will likely differ from the LRT itself (Main & Reserve price feed, Limit, LTV).
* WPT is non-transferrable outside of Gearbox Credit Accounts
* WPT can't be liquidated

## Position unwinding scenario

Consider the case of rsETH leveraged farming with WETH as borrowed token. The position structure is as follows:

* **LLTV:** 95%
* **Collateral:** Equivalent of 50k WETH in rsETH
* **Debt:** 45k WETH
* **Instant liquidity:** 13k WETH
* **Instant liquidity fee:** 0.25% (can be a DEX fee or instant withdrawal tariff)

_Assume that strategy yield is 10% APR on net position value (collateral-debt)._

## Alternative solutions

### Repay full debt with own capital and unstake LRT

The most straightforward way to unwind a position is to repay all debt, withdraw collateral and unstake it. This requires having free capital comparable to the collateral size, which is rarely feasible.

Requirement for capital can be lowered by the amount of instant liquidity in exchange for fee. \
&#xNAN;_&#x54;his will cost 13k \* 0,25% which is equivalent to around **20 days of farming**_

* **Cost:** one redemption period of time (7-14 days) + fees equivalent to 20 days of farming.
* **Requirements:** 32k WETH of free capital

### Iterative withdrawal and repayment

This method has much lower capital requirements, but requires more operations and is more time-consuming.

The example position has Health Factor of 1.06, so part of collateral can be withdrawn without putting position at risk of immediate liquidation. \
Consider that imaginary investor has 1.02 as minimal acceptable Health Factor to have and 5k WETH of free capital.

**Algorithm:**

1. Withdraw maximum collateral up to HF = 1.02
2. Redeem collateral for WETH (wait for redemption period)
3. Repay debt using WETH obtained on Step 2 and free capital
4. If there is any debt remaining move back to Step 1

[Example calculations](https://docs.google.com/spreadsheets/d/1agiBzcpG2ICs7UnCtFkksRCVhqsefytr1wE5ojyrKtY/edit?usp=sharing) show that this scenario takes 6 withdrawal periods (42-84 days).

* **Cost:** 6 redemption periods of time (42-84 days)
* **Requirements:** 5k WETH of free capital

