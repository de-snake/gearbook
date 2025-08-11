# Configuring a Market

## Assets tab

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

{% stepper %}
{% step %}
### Add new asset and set Main Feed

**Asset:** Collateral token address. Select from PriceFeed Store or [add new if needed.](https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/adding-required-price-feeds)

**Price Feed:** Collateral token Main price feed. Select from PriceFeed Store or [add new if needed](https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/adding-required-price-feeds).&#x20;

Main feed is used to for collateral pricing during liquidation checks.
{% endstep %}

{% step %}
### Set Reserve Feed

Select from PriceFeed Store or [add new if needed](https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/adding-required-price-feeds).

{% hint style="success" %}
Used to protect the protocol against manipulations of Main Feeds’ price. See [Dual-oracle pricing](https://docs.gearbox.fi/gearbox-permissionless-doc/competitive-advantages/dual-oracle-pricing) for detailed explanation.
{% endhint %}

{% hint style="warning" %}
Set Reserve Feed equal to Main Feed if you have no other options.\
&#xNAN;_**If reserve price feed is not set, part of the protocol functions (withdrawals, partial liquidations) won't be available.**_
{% endhint %}
{% endstep %}

{% step %}
### Quota limit

Max amount of debt that can be backed by particular asset in the pool. Measured in amount of underlying asset. Used for calculation of Account Value and quota interest rate.\
see [Docs](https://docs.gearbox.finance/overview/liquidations#what-is-a-health-factor) for detailed explanation.
{% endstep %}

{% step %}
### Increase Rate

**Rarely used, feel free to omit**\
When user increases Quota (CA-specific max amount of debt that can be backed by particular collateral), charge a fixed % fee on the quota difference: works like a one-time fee charged on swaps by exchanges.
{% endstep %}
{% endstepper %}

## Rates tab

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

{% stepper %}
{% step %}
### Collateral-specific Rates

See [Collateral-specific rates](../fee-sharing.md) for detailed explanation.

{% hint style="success" %}
Setting IRM in a way that **borrow rate at target utilization (\~80-85%)** equals **60-70% of expected collateral yield** will allow you to bootstrap utilization by allowing favorable rates.\
Equlibrium rate can then be found by increasing collateral-specific rates.
{% endhint %}
{% endstep %}
{% endstepper %}

## IRM tab

<figure><img src="../.gitbook/assets/Screenshot 2025-08-06 at 23.46.29.png" alt=""><figcaption></figcaption></figure>

{% stepper %}
{% step %}
### IRM parameters

Rate curve parameters can be changed after the creation of Market by executing transactions generated from "Change Model" action.
{% endstep %}
{% endstepper %}
