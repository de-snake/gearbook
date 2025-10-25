# Pausable/Unpausable admin

{% hint style="success" %}
## UI for executing Pausable admin functions is located at [https://permissionless-safe.gearbox.foundation/emergency/](https://permissionless-safe.gearbox.foundation/emergency/)
{% endhint %}

## What are pausable and unpausable admins?

Pausable admin can pause active **Pools** and **Credit Managers.**

Unpausable admin can unpause paused **Pools** and **Credit Managers.**

{% hint style="info" %}
Pausable admin is a sensitive role, but its permissions are softer that unpausable admin.\
\
You can set **pausable admin** to be **EOA** to be able to react quickly, but **unpausable admin should be a multisig**.
{% endhint %}

***

## How to add admins?

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F9n0QLqkiJru3BYkpyr8F%2Fuploads%2FcxGLhdfQTtkATg32BHRU%2F0930%20(1).mp4?alt=media&token=accce3fd-67ac-4114-bc26-1a8dd92a3415" %}

***

## Multipause

Multipause is a helper contract that allows pausing multiple Market contracts in one transaction.

{% hint style="warning" %}
For multipause contract to function, you need to add a Multipause contract and at least one Pausable admin to the list.
{% endhint %}

***

## Functions definition

**`Pause Pool(pool)`**

* Pauses pool‑level operations (deposit into pool, withdraw LP tokens)
  * Designed to be combined with Credit Manager pause to prevent bank runs in the most extremal scenarios.

**`Pause Credit Manager(cm)`**

* Pauses all Credit Manager operations.
  * Borrowing, withdrawing collateral, opening & closing credit accounts, performing adapter calls are blocked.
* Only whitelisted **Emergency Liquidators** can liquidate accounts.

**`Pause Market (cm)`**

* Pause Pool and all Credit Managers of a Market.

**`Pause All Contracts (mc)`**

* Pause all Pool and all Credit Managers of a Market Configurator.

***
