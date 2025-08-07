# Creating a new Curator (Market Configurator)

Market Configurator (MC) is a contract that has rights to change parameters of curated Markets. One MC can control multiple markets. The intended usage is for 1 Risk Curator to have 1 MC on each chain they want to deploy on.

### Video explainer

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F9n0QLqkiJru3BYkpyr8F%2Fuploads%2FuR65FqEWMVzqxHTPATPZ%2Fmc%20creation.mp4?alt=media&token=8f5d8f23-e731-4318-bf20-66cefab6f690" %}

{% stepper %}
{% step %}
### Fill in the required parameters

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

* Admin address: \
  The address having the most permissions to execute changes through Timelock \
  &#xNAN;_&#x75;sually Safe multisig or MPC wallet_
* Emergency Admin address: \
  Has permissions to execute the emergency changes without timelock\
  [Permissions list](https://app.gitbook.com/o/-MVf0w9QBIQw5nuscwFc/s/9n0QLqkiJru3BYkpyr8F/~/changes/8/step-by-step-guides/creating-a-new-curator-market-configurator#emergency-admin-permissions).
* Fee Collector address: \
  The address which receives Curator’s share of fee split
* Transaction format: \
  SAFE is likely your to-go choice. Txns are downloaded in Safe-compatible format. The json file can be attached in the Safe Transaction Builder (see [safe explainer](https://help.safe.global/en/articles/234052-transaction-builder)).
{% endstep %}

{% step %}
### Execute transactions in Safe UI

<figure><img src="../.gitbook/assets/Screenshot 2025-06-29 at 20.50.25.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2025-06-29 at 20.51.31.png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Sync Permissionless Interface&#x20;

On Instances Page click on a chain where you've deployed Market Configurator&#x20;

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

Click on a Sync button and wait for Sync to end

<figure><img src="../.gitbook/assets/Screenshot 2025-06-29 at 20.57.33.png" alt=""><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}

<details>

<summary>Emergency Admin permissions</summary>

* Actions in Credit Suite:
  * forbidAdapter
    * Forbids interaction of Credit Accounts with a particular DEX pool or another whitelisted integration
  * forbidBorrowing
    * Forbids creating new positions
  * forbidToken
    * Restricts operations on CAs if at the end of operation there are nonzero forbidden tokens on balance:
      * Can’t increase debt
      * Can’t partially withdraw collateral
      * Can’t interact with adapters
  * pause
    * Forbids all operations with credit accounts. Credit accounts can be liquidated only by whitelisted EmergencyLiquidators
* Actions in Pools:
  * Set limit in Credit Manager to zero:
    * Forbids increasing debt in the given CM
  * Set token limit in Pool to zero:
    * Forbids increasing debt using given token as collateral
  * Pause pool:
    * Forbids deposits and withdrawals in pool
* Actions in PriceOracles:
  * Set priceFeed for given token from PriceFeed Store It can be done if current timestamp > priceFeed allowance timestamp + 1 da

</details>
