# [INTERNAL][MIP-1r4] A new asset class to enforce creator royalties

Created time: November 22, 2022 2:11 PM
Status: Draft

- **Table of contents**

---

# Changelog summary

- Added new TL;DR section, including a rollout schedule.
- Updated new asset class technical architecture from `RoyaltiesNonFungible` to `ProgrammableNonFungible`.
- Updated the royalties distribution/verification logic to be in a separate program outside of `token-metadata`.
- Updated new asset class behavior for extended creator control, incl. adding/removing authorized programs and adding other rules freely.
- Updated migration options for existing NFT collections.
- Updated timeline on self-transfers solution.
- Removed MPLX staking requirements and other penalty mechanisms.

---

# TL;DR

## A new generalized asset class that can be configured to enforce royalties

Metaplex will build a new asset class that allows for flexible configuration of various lifecycle rules, including certain transfer restrictions.

This is how it’ll work at a high-level:

- Metaplex will provide a default set of rules that includes royalties enforcement. These rules can configured by creators.
- Creators may also define custom and/or additional behaviors and rules, including those published by 3rd parties (see MIP-2 for more details).
- Creators can configure the list of trusted programs (i.e. marketplaces) that may transfer the NFTs they create.
- Mint, burn, transfer, delegate, and revoke instructions to be sent to Token Metadata Program instead of SPL Token.

<aside>
📌 For more details about this new asset class outside of the royalties enforcement context, see MIP-2

</aside>

> *Note: The existing `NonFungible` asset class will continue to be supported and projects/creators will now be able to choose the asset class that best fits their use case.*
> 

## Migration

Creators will have different options to migrate existing collections to the new asset class:

1. Creator-initiated migration with a minimum 14-day notice period to collectors.
2. Migration based on a vote organized by the creator for collection holders.

Some of the main benefits of Metaplex’s new asset class are:

- It’s the only solution to represent NFTs natively on Solana — true Master Edition NFTs, no wrapped tokens and therefore native integration with all wallets and marketplaces.
- Collections will be able to migrate in full and all at once — all NFTs in a collection will be of the same asset type, no fragmented collection, no duplicate NFTs or accounts.
- Mint addresses will not need to change, which will ensure stability and compatibility with existing marketplaces and other web3 services (e.g. token and rarity tracking systems).

<aside>
📌 Creators who don’t want to migrate to the new asset class will have the option to remain on the existing `NonFungible` standard. In that case, none of the NFTs in their collection will be eligible for migration.

</aside>

## Other considerations

- Interoperability with existing programs (e.g. staking contracts) is ensured by the control creators have over which programs may interact with the NFTs they create.
- Metaplex Program Library contracts will be updated to ensure compatibility with the new asset class (incl. Candy Machine, Auction House, etc.).
- Self-transfers will be exempt from royalties payments by relying on a new mechanism to link multiple wallets owned by the same person (via Identity NFTs). This wallet linking solution will come to market after the initial release, wallet-to-wallet transfers will not be restricted to start.
- Indexing of the new asset class will be ensured via Metaplex’s Read RPC extension used by wallets and RPC providers (already integrated by GenesysGo, Triton, Solflare, with Phantom, Alchemy, QuickNode coming in Q1 2023).

<aside>
📌 Based on future demand and ecosystem feedback, we may create additional protocol-level verification and distribution of royalties payments.

</aside>

## Rollout schedule

1. Draft program interfaces available for public review [December]
2. Devnet available for integration development by marketplaces, wallets, dApps [December]
3. Auction house support [December]
4. Publicly available for migration [Early January]
5. Candy machine support [January]

---

# Background

On the back of cascading announcements of zero royalty marketplaces for traders, the Solana NFT community is at an inflection point for creator monetization and the future of royalties. In this document, we propose the creation of a new asset class in Token Metadata that will realign creators with their communities by providing an on-chain solution for enforcing royalties.

**Our previous announcement on royalties:**

[**Royalties and the Future of Creator Monetization [Public]**](https://www.notion.so/Royalties-and-the-Future-of-Creator-Monetization-Public-5fdcd1b163084b9b87b2e90090129d22) 

---

# Solution framing

The creation of a new asset class is the most viable solution to provide NFT creators with a reliable way to enforce royalties, without compromising the collector experience. This new asset class will coexist with NFTs as we know them today and we expect both asset classes (and more in the future) to be used concurrently across the ecosystem.

## Primary needs

- Provide a reliable way to creators to receive royalties payments on the sale of NFTs they create.
- Be usable for both new and existing NFTs and NFT collections.
- Exonerate NFTs from royalties payments when moving between wallets owned by the same person
- Minimize new development work for ecosystem developers and partners to adopt (e.g. existing wallets, marketplaces, etc.).
- Be as compatible as possible with other ecosystem solutions (e.g. custodial staking contracts, NFT DeFi projects).
- Minimize centralized trust assumptions and maximize creator control.

## Introducing a new generalized asset class that can be configured to enforce royalties

Metaplex will build a new asset class that allows for flexible configuration of various lifecycle rules, including certain transfer restrictions. The first application of this new asset class will be creator royalties enforcement.

For more technical details about the new generalized asset class and its future applications, you can refer to **MIP-2**.

## The new `ProgrammableNonFungible` asset class applied to royalties enforcement

Metaplex will provide a default set of rules that enable royalties enforcement on the new `**ProgrammableNonFungible**` asset class. Those rules can configured by creators.

This is an overview of how the new asset class will be used to enforce royalties:

- Metaplex will provide a default set of rules and programs that enforce royalties for convenience. This will enable the new asset class to enforce royalties out of the box (i.e. without any extra work on creators).
- Creators will be able to add/remove/configure rules and programs authorized to transfer the NFTs they create without restrictions. Creators will be responsible for monitoring the additional programs they decide to include. **Creators should only add programs that they trust will honor royalties payments.**
- Transfers to and from the `UpdateAuthority` of the NFT or collection (typically the creator) can be exempt from royalties payments if the creator allows that as a rule.
- Mint, burn, transfer, delegate, and revoke instructions to be sent to Token Metadata Program instead of SPL Token so the rule sets can be applied.

For more information about custom and/or additional behaviors and rules (incl. third-party rules), see **MIP-2**. Creators may choose to use other rule sets, however their behavior are not guaranteed to be royalties-compliant.

> **Note on self-transfers**
*Since the rules required to enforce royalties payments would restrict transfers to certain programs and use cases, an exception might need to be carved out to accommodate for self-transfers (i.e. moving an NFT between two wallets a same person owns). We are exploring a wallet-linking solution to solve for this use case. A new, non-transferrable Identity NFT that allows wallet linking could ensure that a person owning multiple wallets transfer NFTs between those wallets with minimal friction (more details below).*
> 

## Extending Token Metadata

Token Metadata is responsible for the creation of over 99% of NFTs on Solana and provides the standard for how metadata is attached to Solana based tokens.

Some of the main benefits of Metaplex’s new asset class are:

- It’s the only one to represent NFTs natively on Solana — true Master Edition NFTs, no wrapped tokens and therefore native integration with all wallets and marketplaces.
- Collections will be able to migrate in full and all at once — all NFTs in a collection will be of the same asset type, no fragmented collection, no duplicate NFTs or accounts.
- Mint addresses will not need to change, which will ensure stability and compatibility with existing marketplaces and other web3 services (e.g. token and rarity tracking systems).

> *Note: The existing `NonFungible` asset class will continue to be supported and projects/creators will now be able to choose the asset class that best fits their use case.*
> 

---

# Using `ProgrammableNonFungible` **assets to enforce royalties `[WIP]`**

At a high-level, the new `ProgrammableNonFungible` asset class allows for flexible configuration of rules and behaviors related to various lifecycle events (e.g. transfer, delegate, burn, etc.). The first application of the new `ProgrammableNonFungible` ****asset class is royalties enforcement.

### How to detect a `ProgrammableNonFungible` that implements a royalty enforcement

Currently NFTs on Solana have a Token Standard and a Major Specification version. We can use the combination of `SpecificationVersion` and `TokenStandard` to create an `interface` or `asset class`. More information can be found in MIP-2

```rust
#[repr(C)]
#[cfg_attr(feature = "serde-feature", derive(Serialize, Deserialize))]
#[derive(BorshSerialize, BorshDeserialize, PartialEq, Eq, Debug, Clone, FromPrimitive)]
pub enum TokenStandard {
	NonFungible,        // This is a master edition
	FungibleAsset,      // A token with metadata that can also have attrributes
	Fungible,           // A token with simple metadata
	NonFungibleEdition, // This is a limited edition
	
	**ProgrammableNonFungible**,
	
}
```

In the examples above you can see that V1 NonFungible maps to the V1NFT interface. In the Read API this would surface as **Interface::V1ProgrammableNonFungible.**

## Integration TL;DR for `ProgrammableNonFungible` assets

1. Transfer instructions (and other spl-token instructions) are now sent to Token Metadata instead.
2. The `rules_account` can be easily discovered on chain using account derivation or via the Metaplex Read API, an RPC indexing extension run by many existing RPC providers.
3. TokenMetadata will expose new instructions under a new simplified API.
    1. For example `CreateMetadataAccount` and  `UpdateMetadata` are replaced with `mint` and `update`
    2. These instructions take versioned payloads, this makes it easier to adopt updates and maintain the code
        1. For Example `MintV1 {...}` , `MintV2`

### Discovering Rules Account

```rust
// --- Without READ API

// For Collections
1. Derive RuleLink PDA with collection id.
2. Get RuleLink PDA -> Rules Account

// For Individual Nfts with no collection
1. Derive RuleLink PDA with mint id.
2. Get RuleLink PDA -> Rules Account

// --- With Read Api
Rules Account and parsable rules will be served form the read api
```

### Creating a Royalty-Enforced NFT

```rust

// Pseudo Code
let mint = Pubkey;
let metadata = Pubkey
let update_authority = Pubkey
let rules_account = Pubkey
let data = Metadata {
  uri,
  name,
	symbol
...
	data
...
}
let payer = Pubkey
let owner = Pubkey

let instruction_data = MintInstruction::V1 {
	mint: AccountIndex(0),
...
	owner: AccountIndex(3),
	payer: AccountIndex(2),
...
	collection: AccountIndex(8)
...
	token_standard: TokenStandard
};

let accounts = [
	mint,
	metadata,
	payer,
	owner,
	owner_token_account,
	rules_account,
	update_authority,
	collection_mint,
	collection_metadata,
	system_account
];

Transaction(Instruction(instruction_data, accounts), signers: [payer]);

```

### Allow-listed marketplace listing an NFT for sale (escrowless)

```rust
// Pseudo Code

// escrowless: owner delegates to marketplace 
// Pseudo Code
let mint = Pubkey;
let metadata = Pubkey
let update_authority = Pubkey
let rules_account = Pubkey
let data = Metadata {
  uri,
  name,
	symbol
	...
	data
	...
}
let payer = Pubkey
let owner = Pubkey

let instruction_data = Delegate::V1 {
...
	owner: AccountIndex(4),
	payer: AccountIndex(3),
...
	delegate: AccountIndex(2)
...
	delegate_role: DelegateRole::Sale // DelegateRole::Utility <--- can be set to only allow original owner transfer while delegated
};

let accounts = [
	mint,
	metadata,
	delegate,
	payer,
	owner,
	owner_token_account,
	rules_account,
	system_account
];

Transaction(Instruction(instruction_data, accounts),signers: [payer, owner]));

// Delegate is now the only one that can transfer the NFT until 
// revoke() is called by the owner.
// delegate() called while delegating will move the delegation to the new_delegate if the owner is signing

```

### Allow-listed marketplace listing an NFT for sale (escrowed)

```rust
// Pseudo Code
// escrow: owner transfers via token metadata to escrow marketplace
//
// If the auth rules allow blanket transfers to a program then the 
// program can have the nft sent to a pda of that program, and then 
// transferred by that program to system keypairs

let mint = Pubkey;
let metadata = Pubkey
let update_authority = Pubkey
let rules_account = Pubkey
let data = Metadata {
  uri,
  name,
	symbol
	...
	data
	...
}
let payer = Pubkey
let owner = Pubkey
let new_owner = PDAOfProgram

let instruction_data = Transfer::V1 {
...
	owner: AccountIndex(4),
	payer: AccountIndex(3),
...
	new_owner: AccountIndex(2)
};

let accounts = [
	mint,
	metadata,
	new_owner,
	payer,
	owner,
	owner_token_account,
	rules_account,
	system_account
];

Transaction(Instruction(instruction_data, accounts),signers: [payer, owner]));
```

### Wallet transferring NFT to another wallet

```rust
// Pseudo Code

// wallets call token metadata to transfer instead of spl-token

let mint = Pubkey;
let metadata = Pubkey
let update_authority = Pubkey
let rules_account = Pubkey
let data = Metadata {
  uri,
  name,
	symbol
	...
	data
	...
}
let payer = Pubkey
let owner = Pubkey
let new_owner = Pubkey

let instruction_data = Transfer::V1 {
...
	owner: AccountIndex(4),
	payer: AccountIndex(3),
...
	new_owner: AccountIndex(2)
};

let accounts = [
	mint,
	metadata,
	new_owner,
	payer,
	owner,
	owner_token_account,
	rules_account,
	system_account
];

Transaction(Instruction(instruction_data, accounts),signers: [payer, owner]));
```

### Escrowless staking program staking

```rust
// Pseudo Code

// In this scenario the staking program freezes the token 1 day after being staked 

// Owner calls delegate with 
...
	delegate_role: DelegateRole::Utility 
};

let mint = Pubkey;
let metadata = Pubkey
let update_authority = Pubkey
let rules_account = Pubkey
let data = Metadata {
  uri,
  name,
	symbol
	...
	data
	...
}
let payer = Pubkey
let owner = Pubkey
let delegate = Pubkey
let instruction_data = Freeze::V1 {
...
	owner: AccountIndex(4),
	payer: AccountIndex(3),
...
	delegate: AccountIndex(2)
...
	delegate_role: DelegateRole::Utility // DelegateRole::Utility <--- can be set to only allow original owner transfer while delegated
};

let accounts = [
	mint,
	metadata,
	delegate,
	payer,
	owner,
	owner_token_account,
	rules_account,
	system_account
];
//Delegate signs this one
Transaction(Instruction(instruction_data, accounts),signers: [payer, delegate]));
```

---

# `Identity` NFTs & wallet linking

<aside>
📌 This section describes a new asset class that would be introduced to enable free transfers between two wallets owned by the same person. This scope of work will not be included in the initial release of `ProgrammableNonFungible` as the solution to creator royalties enforcement.

Metaplex’s wallet linking solution may come to market later depending on ecosystem demand and feedback from creators and collectors. Initially, wallet-to-wallet transfers will not be restricted.

</aside>

## Trade-offs between royalties enforcement and freely transferrable tokens

Any solution that reliably enforces creator royalties will have to apply a set of restrictions on NFT transfers (either by only allowing certain programs to transfer the NFT or by validating that royalties are being paid as part of the sale transaction).

Unfortunately one cannot assume that all transfers should incur royalties since not all transfers represent NFT sales — For example one person sending an NFT from their hot wallet to their cold storage is a transfer that shouldn’t incur royalties payments.

This is a particularly tricky problem to solve because the solutions that would guarantee creator royalties payments are diametrically opposed to the simplest user experience when it comes to friction-less self-transfers.

One on end, there are zero restrictions on transfers but creator royalties payments are easy to evade. On the other end, creator royalties are always guaranteed to be paid but the experience to make a simple self-transfer is a lot more cumbersome. Metaplex aims to try to find a balance between those two extremes by soliciting community feedback.

Metaplex’s proposed solution is to create an asset class that enables people to link multiple wallets they own — transfers between linked wallets would then always be free of royalties payments. For this solution to be viable, it needs to be difficult to be abused by malicious marketplaces and other actors who might want to utilize wallet linking as a way to bypass paying creator royalties.

## Wallet linking as a new asset class (Identity NFTs)

The Identity NFT is a new asset class introduced alongside `ProgrammableNonFungible` that will enable free transfers between wallets owned by the same person.

```rust
#[repr(C)]
#[cfg_attr(feature = "serde-feature", derive(Serialize, Deserialize))]
#[derive(BorshSerialize, BorshDeserialize, PartialEq, Eq, Debug, Clone, FromPrimitive)]
pub enum TokenStandard {
NonFungible,        // This is a master edition
FungibleAsset,      // A token with metadata that can also have attributes
Fungible,           // A token with simple metadata
NonFungibleEdition, // This is a limited edition

ProgrammableNonFungible,

NonTransferrable,

**Identity**
}
```

## Important considerations about Identity NFTs

Linking wallets to identities is the first step in functionality for delegated signing or ownership.

As it relates to royalty enforcement, the following rules will apply:

- They are non-transferrable (but may be burned).
- They may only have up to N wallets linked (e.g., 5).
- They may require a minimum number of filled fields to become eligible for free transfers (e.g., the user must set an avatar using an NFT contained in the wallet, connect one social media account, etc.).
- The fields may optionally be filled by third-party integrations such as KYC providers or other identity solutions.
- A given wallet may only be linked to a single identity (to prevent daisy-chaining and other possible abuse vectors associated with reusing wallets).
- Linked wallets may not be PDAs (which makes it more likely wallets belong to humans).
- Time-based restrictions will apply to linking and unlinking wallets to prevent automated abuse (e.g. linked wallets only become usable 24h after being linked, cool-down period of N days after a wallet is unlinked and the slot can be reused, etc.).

Additional schemes may be introduced in the future depending on the ecosystem behavior observed — for example, allowing royalty-free transfers to and from the creator wallet (the update authority for an NFT).

## Creating identities & linking wallets

Metaplex will create a simple dApp that allows users to associate some data with their identity NFT.

### **Required fields to create an identity NFT**

- Set an avatar `image` using an NFT contained in the wallet.
- Some level of account verification (e.g., must connect 1 of N social accounts). This may integrate with third-party protocols in the future (e.g., Civic).

### **Linking additional wallets**

Once the Identity NFT is created, people may link additional wallets with the following requirements:

- Proof of wallet ownership and Identity ownership must happen within a short time window in the same user session.
- See above for additional linked wallet restrictions.

After a wallet is linked to an Identity token, transfers between the linked wallets are allowed without royalty restrictions. This can happen in wallets directly or anywhere else (e.g., web3 games).

### Obfuscation of Linked Wallets

Metaplex is exploring ways to hide the on-chain relationships between wallets via hashing or ZK proofs.

---

# Collection migration

## Possible migration paths for existing collections

Metaplex’s solution makes it possible for the majority of existing collections to migrate to the new `ProgrammableNonFungible` asset class to enforce creator royalties.

Creators who choose to migrate to the new `ProgrammableNonFungible` asset class will have the following options to do so:

- **Unilateral migration with a minimum 14-day notice period to collectors.**
    1. Creators would be required to publicly announce their intention to migrate to the new asset class to the holders of their collection.
    2. A minimum 14-day notice period would be required to ensure that collectors are informed ahead of time.
    3. Once the notice period ends, the creator would be able to unilaterally migrate all NFTs in their collection to the new `ProgrammableNonFungible` asset class.
- **Migration based on a vote organized for collection holders.**
    1. A creator would organize a vote via their DAO or another transparent mechanism for the current NFT holders. If the vote passes, the entire collection can be migrated by the creator.
    2. There would be specific Protocol-level guardrails or vote requirements to be met to ensure the current NFT holders have a fair chance at voting.
    3. Prerequisite for vote-based migration: Using Metaplex’s sized collections standard would be required so the smart contracts can calculate the quorum and passing votes percentages based on the number of NFTs in the collection.

<aside>
📌 Creators who don’t want to migrate to the new asset class will have the option to remain on the existing `NonFungible` standard. In that case, none of the NFTs in their collection will be eligible for migration.

</aside>

## Example of a creator-led vote

A creator could utilize Realms, a UI built on Solana’s `spl-governance` protocol that provides an out-of-the-box way for NFT communities to create DAOs and allow a collection’s NFT holders to vote on an issue.

In order to use this solution, NFT projects would be required to:

1. Conform to the Metaplex Collections Standard (incl. the use of sized collections).
2. Value each NFT in the collection as an equal vote.
3. Determine a quorum threshold, and separately, a passing % of votes. *Quorum threshold and passing % may have dramatic impacts on the voting outcome.*
4. Create a non-binding vote for collection holders on whether a migration should occur.
    
    > *Note: In the future Metaplex could build an automated process for such a voting mechanism where collections may execute the upgrade themselves.*
    > 
5. Assign proof of collection ownership to the DAO for trust-less verification of the community’s intent to migrate. The exact mechanism is TBD but likely to be update authority or DAO ownership of the Collection NFT.

spl-governance interoperability will continue after a collection is migrated since the voting mechanism is escrow-less.

---

# Interoperability with ecosystem programs & dApps

## Built-in support via main Metaplex programs

To ensure continuity, Metaplex will support the new `ProgrammableNonFungible` asset class in its main programs:

- Candy Machine (the method by which the majority of new Solana NFTs are minted)
- Fixed Price Sale (the contract used to created 1/1s and editions)
- Auction House (protocol for marketplaces to implement a decentralized sales contract)

The `ProgrammableNonFungible` assets will also be compatible with any escrow-less utility program, like `Hydra` or `spl-governance`.

## Compatibility with escrow-based programs

Escrow-based programs will function as today provided that creators authorize those programs to transfer `ProgrammableNonFungible` assets.

**Escrow based programs must update to send transfer instructions to the Token Metadata program instead of** `spl-token`

For example if an NFT project set up a staking contract for their holders to stake NFTs and receive rewards, the creator will be able to include that program ID in the list of authorized programs for their collection for staking to continue working as with `NonFungible` assets (the majority of NFTs currently on Solana).

## Indexing

Indexing should be straightforward for any project using Metaplex’s Read RPC extension (already integrated by GenesysGo, Triton, Solflare, with Phantom, Alchemy, QuickNode coming in Q1 2023). The new asset types will appear automatically and integrators need only to start reading the new Enum types; this is also true for compressed NFTs.

For those not using the Read RPC extension, modifications to existing indexers should be simple by reading the existing `TokenStandard` field in order to determine the type of NFT being indexed.

---

# Further Explorations

Here’s a short list of additional related topics that we’re actively exploring, related to hardening this new asset class and accelerating its adoption.

**Additional protocol-level verification and distribution of royalties payments**

Based on future demand and ecosystem feedback, we may create additional protocol-level verification and distribution of royalties payments alongside the Token Metadata program. Creators would be able to use this option to allow open, trust-less, escrow-less access to liquidity for their collections while ensuring royalties distributions are enforced or verified on-chain.

The technical underpinning of the solution is to allow collectors to specify delegate types while delegating (i.e. signaling their intent for a delegation). `Sale Delegate` would be a specific delegate type that would be made available via the `ProgrammableNonFungible` asset class. It would then be used in conjunction with the royalties enforcement rule set to only allow programs that meet the requirements of on-chain royalties verification to transfer the NFT (the creator would still need to explicitly list those programs in the list of authorized programs).

This approach would provide a way for NFT collections to access open liquidity without requiring creators to make trust-based assumptions about individual programs.

**Open liquidity**

As part of the new Sale Delegate instruction, Metaplex could add ways to allow any program to execute the sale, effectively creating a shared global liquidity pool for listed NFTs.

If trading liquidity is high enough, market dynamics could remove the need for managed lists of [royalties-compliant programs](https://www.notion.so/INTERNAL-MIP-1-A-new-asset-class-to-enforce-creator-royalties-728fd05ef7274b06b86479b5f92a2366). For example if a marketplace tried to evade creator royalties by listing an NFT at an abnormally low price in an open liquidity market (and then settle the transaction for a different price outside of the royalty-enforced system), the asset would quickly get sniped and cancel out any potential gains for the malicious marketplace.

> *Note: This would be an opt-in feature for marketplaces, creators and collectors.*
> 

---

# Conclusion

Given overwhelming creator support and feedback, Metaplex is optimistic that we can all build our way to a better future where royalties are broadly supported and the incentive alignment between creators and their communities is preserved.

If you’re a creator or a developer who’s interested in helping pioneering this new standard or looking to migrate your existing collection, please send us an email at **[creators@metaplex.com](mailto:creators@metaplex.com)** or DM us [**@metaplex**](https://twitter.com/metaplex) with any feedback, we’d love to connect.
