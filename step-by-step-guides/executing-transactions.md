# Executing transactions

After the changes in GIP were tested and are ready to be executed onchain, go to the GIP page and click "Finalize GIP".

{% hint style="info" %}
If the only button you see is "Reopen for Changes", click it and you will be able to finalize the GIP again.
{% endhint %}

<figure><img src="../.gitbook/assets/Screenshot 2025-08-08 at 11.43.06.png" alt=""><figcaption></figcaption></figure>

### How to set Earliest Execution Date?

The default timelock is 24h, so you need to get signatures in Owner Multisig before **Earliest Execution Date - 24h.**&#x20;

E.g. if it takes 2h for you to get needed signatures, set **Earliest Execution Date** to _**current time + 2h + 24h.**_

## Executing with Gearbox open-sourced Safe Permissionless UI

After finalizing the batch link to the Safe UI with prepared txs will appear.

<figure><img src="../.gitbook/assets/Screenshot 2025-09-26 at 16.28.03.png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
[Permissionless Safe](https://docs.gearbox.fi/gearbox-permissionless-doc/competitive-advantages/essential-tooling-for-curators#permissionless-safe) is an open-source, IPFS-hosted version of the Safe Multisig UI designed to review and sign transactions securely in a human-readable format. It eliminates backend dependencies to mitigate risks like Bybit-type attacks and performs checks of IPFS CID signature to prevent phishing.
{% endhint %}

### Transactions' lifecycle

<figure><img src="../.gitbook/assets/timeline (2).jpg" alt=""><figcaption></figcaption></figure>

### Queuing transactions

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F9n0QLqkiJru3BYkpyr8F%2Fuploads%2Fyb33s6xLnXsLKLpRTyWw%2Fgip%20finalization.mp4?alt=media&token=02949fc6-5b9b-42f0-9926-da454ee91015" %}

## Executing transactions

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F9n0QLqkiJru3BYkpyr8F%2Fuploads%2FD996Q64luHv4QiwGPr9o%2FScreen%20Recording%202025-09-26%20at%2016.22.38.mp4?alt=media&token=560c82f9-1526-4a0e-b9f7-e7db93e75534" %}
