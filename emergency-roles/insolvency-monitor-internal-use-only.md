---
hidden: true
---

# Insolvency monitor (Internal Use only)

Insolvency Monitor is a service that checks markets' solvency on each block and has access to Pausable Admin Private Key to pause the market in case of alert.

Its core logic is pretty simple:

* For each market:
  * Calculate collateral value on all Credit Accounts discounted by liquidation premium
  * Require Discounted Collateral Value to be no less than Market's outstanding debt

It's strongly recommended for each curator to run an own instance of Insolvency Monitor.

If a fallback instance ran by Gearbox is required, pls reach out to the team.
