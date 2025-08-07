---
hidden: true
---

# Governance structure

Cross Chain Multisig (CCM)

Instance Owner (IO)

Bytecode Repository (BCR)

Credit Account (CA)

## Roles

### DAO (token holders)&#x20;

1. Pre on-chain governance
   1. Holders vote on snapshot for human-readable description of changes and links to files with transactions and corresponding checksums
   2. Technical Multisig signers sign transactions on Mainnet to upload batches to Cross Chain Multisig
   3. Cross Chain Multisig signers sign transactions on Mainnet for them to become executable on another chain
   4. Signed batch is executed on target chain
2. Post on-chain governance
   1. Holders vote on snapshot for human-readable description of changes and smart contracts upload batches to Cross Chain Multisig contingent on voting result
   2. Cross Chain Multisig signers sign transactions on Mainnet for them to become executable on other chains
   3. Signed batch is executed on target chain

In the current implementation, signers are trusted not to deviate and only sign batches submitted by Gearbox DAO on Ethereum Mainnet. In future versions, DAO decisions will be propagated to other chains using bridges or `L1SLOAD`.

**Potential deviation from expected scenario:** \
CCM signers can create and sign unauthorized batches off-chain and execute them on chains different from Mainnet, because the current implementation does not enforce that the batch was submitted and approved on Ethereum Mainnet — it only checks for valid signatures and a valid batch structure.

**However** CCM's permissions are very limited and malicious behaviour can't harm existing users.

### Cross-Chain multisig

**Permissionless Curation Contracts** are designed to enable the Gearbox Protocol to function fully without active DAO involvement, with DAO influence restricted at the smart-contract level. The design follows these key principles:

* **Non-Interference with Decisions**: The DAO cannot influence or override decisions made by Curators or Instance Managers.
* **No Control Over Market Contracts**: Market contracts' parameters allow flexible modification by Curators, but the DAO cannot alter them.
* **Exclusive Control Over System Contract Versions**: Only the DAO can authorize new versions of system contracts (core protocol logic) for use. Adding adapters, price feeds, bots, or other components remains permissionless.
* **Chain Expansion Oversight**: Only the DAO can activate Gearbox on new chains, ensuring the correct Treasury address and Instance Owner multisig are set.

Allowed actions:

1. Globally for all chains (in BytecodeRepository)
   1. Allow System contracts for usage
   2. Add & remove auditors
   3. Add public domains & contract types (UX and DX improvement)
2. Locally on target chain (in InstanceManager)
   1. Activate Instance (chain) by setting Instance Owner and Treasury addresses; once granted, this roles can't be revoked by DAO
   2. Deploy system contracts
   3. Set global addresses and configure global contracts\
      Examples of global contracts: Bytecode repository, GEAR staking

None of the allowed actions can modify behaviour of existing Markets.

### Instance Owner

The Instance Owner role is designed as a soft power mechanism to ensure Curators have access to a comprehensive and up-to-date list of chain-specific parameters, properly configured for each network.

The Instance Owner multisig initially includes 3 core Gearbox contributors and 9 Technical Multisig participants (crypto-founders and protocol supporters), with a signature threshold of 4. The goal is to include all relevant Curators and chain contributors as signers to prevent excessive censorship and  competition within the Instance Owner multisig.

Allowed actions:

1. Price feed store
   1. Allow/ forbid feeds to be used for particular tokens
   2. Configure allowed Price Feeds' parameters
2. AccountFactory
   1. Rescue CAs: execute calls from the account that is not used by anyone.
3. BotList
   1. Forbid a Bot do disable attaching it to CAs
4. Router
   1. Configure chain-specific parameters

None of the allowed actions can modify behaviour of existing Markets.

Some of the offchain services (front-end, liquidator, monitoring tools) rely on proper configuration of Router and can stop working if router state becomes incorrect.

### Curator

#### Market Configurator Admin

Allowed to change critical parameters of the market that can affect existing LPs and Borrowers.

Timelock of at least 24h is forced.

#### Emergency Admin

Can perform limited list of sensitive actions which can affect existing LPs and Borrowers without timelock. Including but not limited to pausing parts of the market, changing price feeds of tokens.&#x20;

#### Pausable admin

Can pause parts of the market without timelock. Can affect existing LPs and Borrowers.

## Curators' tools and interfaces

### Permissionless Interface

* **Demo:**

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F9n0QLqkiJru3BYkpyr8F%2Fuploads%2FNanWPyWjWeYcVHjUKlJQ%2Fwhole%20flow.mp4?alt=media&token=152a96d8-9927-425c-b657-cbce5669e7b0" %}

* **URL**: [https://permissionless-staging.gearbox.foundation/curators](https://permissionless.gearbox.foundation/curators)
* **Purpose**: Enables curators to create transaction batches for market deployment and configuration using human-readable tables. The interface generates transaction data, which is uploaded to IPFS, with the Content Identifier (CID) signed by the GIP creator to prevent phishing.\
  Will also include pages that allow to run various tests to check correctness of transactions and resulting state.&#x20;
* **Note**: This interface can't modify onchain state directly, but just creates transactions that can be later signed by curator; it consists both of a frontend and backend both of which can be compromised. Therefore it shouldn't be perceived as guarantee of transactions or state correctness or its safety for end users.

### Permissionless Safe

Takes unique identifier (CID) of file with transactions uploaded to IPFS using Permissionless Interface, allows to read txs in human-readable form and sign them.

* **Demo:**

{% embed url="https://files.gitbook.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F9n0QLqkiJru3BYkpyr8F%2Fuploads%2Fyb33s6xLnXsLKLpRTyWw%2Fgip%20finalization.mp4?alt=media&token=02949fc6-5b9b-42f0-9926-da454ee91015" %}

* **Repository**: [https://github.com/Gearbox-protocol/permissionless-safe](https://github.com/Gearbox-protocol/permissionless-safe)
* **Example UI:** [https://permissionless-safe.gearbox.foundation/txs/?cid=bafkreierlnbtoxczkyk3zd5ozimxtrp4vol3rhfwrjtgk52vo7qyjs2fwe](https://permissionless-safe.gearbox.foundation/txs/?cid=bafkreierlnbtoxczkyk3zd5ozimxtrp4vol3rhfwrjtgk52vo7qyjs2fwe)
* **Purpose**: An open-source, IPFS-hosted version of the Safe Multisig UI designed to review transactions in a human-readable format and sign transactions them onchain. It eliminates backend dependencies to mitigate risks like Bybit-type attacks and performs checks of IPFS CID signature to prevent phishing.
* **Note**: The open-source nature and IPFS hosting ensure users can verify the code's integrity.\
  However it shouldn't be perceived as guarantee of transactions or state correctness or its safety for end users.

