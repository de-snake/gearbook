# Collateral-specific rates

### Problem

Multicollateral lending protocols like Aave and Euler use a single interest rate curve to determine borrow rates for all collaterals, despite varying demand for each collateral type. This leads to issues, particularly when the supply cap for a specific collateral is low compared to lending-side TVL in the pool:

* **Underpricing of High-Demand Loans**\
  Loans against collaterals with low supply caps minimally affect the pool's overall utilization rate
* **Underpayment of Lenders and Curators**\
  Lenders and curators receive lower returns, effectively subsidizing borrowers who secure loans against these constrained collaterals
* **Curators are involved in high-frequency capital reallocation**\
  As of 06/06/2025 just a single "MEVCapital USDC" Morpho vault had executed 3595 reallocation transactions operations since its deployment date of 07/24/2024 ([source](https://dune.com/queries/5244280)).

### Solution

Curator controls individual rates for collaterals to better adjust to their demand and supply dynamics. —&#x20;

* _**Rate discovery efficiency**_ of isolated market designs (e.g., Morpho, Silo)\
  Rates in different markets are set independently for different collaterals
* **User experience and capital efficiency** of multicollateral designs (e.g., Aave, Euler)\
  Curators don't need to participate in capital allocation process
* **Rate Adjustment Frequency**: Curators can update rates for each collateral no more frequently than once every 24 hours and can self-enforce longer intervals if desired.

This approach combines _**efficiency of rate discovery**_ of the isolated markets design (e.g. Morpho, Silo)  and _**UX and capital efficiency**_ of multicollateral design (e.g. Aave, Euler).
