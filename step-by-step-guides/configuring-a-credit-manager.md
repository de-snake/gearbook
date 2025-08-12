# Configuring a Credit Manager

## _**Setup examples**_

[ setup example (BNB chain: USD1 pool, USDX collateral)](https://www.notion.so/Adapter-setup-example-BNB-chain-USD1-pool-USDX-collateral-208145c16224807fa1a0d318c01bc1ae?pvs=21)

[setup example (Ethereum chain: tBTC pool, uptBTC collateral)](https://www.notion.so/Adapter-setup-example-Ethereum-chain-tBTC-pool-uptBTC-collateral-20e145c1622480c886d8d43dc5e9f5bb?pvs=21)

[setup example (Ethereum chain: USDC pool, frxUSD/USDf collateral)](https://gearboxprotocol.notion.site/Adapter-setup-example-Ethereum-chain-USDC-pool-frxUSD-USDf-collateral-24c145c16224809d80d2d171e1128317?source=copy_link)

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

