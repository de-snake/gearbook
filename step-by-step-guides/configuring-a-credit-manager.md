# Configuring a Credit Manager

## _**Collaterals**_

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

{% stepper %}
{% step %}
### _**Add new collateral**_

Select token from those already added to Market. If not present, [add token to Market.](https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/configuring-a-market#add-new-asset-and-set-main-feed)

Set LT of a collateral - Liquidation Threshold (same as Liquidation LTV on other lending protocols)

{% hint style="info" %}
LT can't be higher than 100% - liquidation Fee - liquidation Premium
{% endhint %}
{% endstep %}

{% step %}
### Modify LT of existing collateral

LT can't be changed immediately, only through a gradual linear ramp from current LT to target LT that starts when transactions are executed onchain (duration of ramp can be set in UI).

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}

## _**Adapters**_

[_**Detailed section on adapters configuration.**_](https://docs.gearbox.fi/gearbox-permissionless-doc/step-by-step-guides/configuring-adapters)

<div data-full-width="false"><figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure></div>
