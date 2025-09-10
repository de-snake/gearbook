# Seamless LP migration

## Purpose

This LP migration contract is designed to allow users migrate liquidity without monitoring the pools for available liquidity:

* Designed for the case where immediate migration is not possible due to liquidity constraints.
* Users can pre-sign their intention to migrate by granting allowance to the migration contract.
* The migration will be executed by the instance owner multisig as soon as liquidity becomes available.



In other words, this contract is a safe automation tool:

* You lock in your intent to move from the old pool to the new one.
* You don’t have to monitor liquidity or time the transaction yourself.
* The migration will happen at the first opportunity.

***

### How it Works

There are only two functions in the migration contract:

1. User function (allowance setup)
   * You give the migration contract allowance for your LP tokens in the old pool.
   *   This does not move funds immediately — it only means:

       > “Whenever possible, please take my LP tokens from the old pool and put them into the new pool.”
   * After signing, you are done.
2. Instance owner function (execute migration)
   * Can only be called by the instance owner multisig (chain-specific). However, instance owner can't do anything except for migrating liquidity between the pools specified by user.
   * Once liquidity becomes available, they trigger the migration:
     * LP tokens are redeemed from the old pool.
     * Assets are deposited into the new pool on behalf of the user.
   * Both _old pool_ and _new pool_ are fixed parameters of the contract and cannot be changed.

***

### Safety of Allowance

* **Immutable destination:** your funds can only move old pool → new pool.
* **No arbitrary spending:** allowance is strictly limited to the old pool LP tokens.
* **Controlled execution:** the migration logic is minimalistic and fixed in contract. Even if instance owner multisig goes malicious, its actions can't result in user losing money.

***

### Migration Lifecycle

1. User grants allowance
   * Approves their LP tokens to be used by migration contract.
2. Monitoring phase
   * Liquidity in old pools may be fully utilized (100%).
   * Gearbox contributors monitor until withdrawals are possible.
3. Execution phase
   * Instance owner calls the migration function at the first chance.
   * Funds are moved automatically on behalf of the user who granted the allowance.
4. Completion
   * Users now hold LP tokens in the new pool.
   * Yield continues seamlessly.
