# **[MIP-1] A new asset class to enforce creator royalties**

📣 **Creators can now start the royalties enforcement upgrade process for existing collections at [royalties.metaplex.com](http://royalties.metaplex.com/) (beta).**

**[Integration guide for developers](https://github.com/metaplex-foundation/metaplex-program-library/blob/master/token-metadata/program/ProgrammableNFTGuide.md) | [Royalties FAQs](https://metaplex.notion.site/metaplex/Public-FAQ-A-new-asset-class-to-enforce-royalties-4662d26ee8af451faeb16d6a0534cb70)**

## Overview

Metaplex is building a new asset class, Programmable NFTs, that allows for flexible configuration of various lifecycle rules, including certain transfer restrictions that can be used by creators to enforce royalties. The new asset class is called Programmable NFTs.

> 📌 The existing `NonFungible` asset class will continue to exist and projects/creators will be able to choose the asset class that best fits their use case. We recognize that not all collectors will want to use `ProgrammableNonFungible` assets because of the control it provides creators and advise creators to seriously weigh the pros and cons.
> 

Here is how the new asset class will work at a high-level:

- Programmable NFTs can include “rule sets” that can be configured by creators. Creators will be able to enable royalties enforcement by specifying in these rule sets which programs may transfer their NFTs.
- Mint, burn, transfer, delegate, and revoke instructions will be sent to Token Metadata Program instead of SPL Token in order to validate against creator applied rule sets.
- There are reasonable arguments about whether allow-list or deny-list based approaches to royalty enforcement are preferable, and how these lists should be governed, managed or updated. Programmable NFTs support both approaches and provides optionality to creators. More on the tradeoffs in "Upgrade implications and risks.”
- The Metaplex Foundation will provide an optional rule set based on an allow-list that will be updated periodically to only include programs that pay creator royalties for convenience. Creators are free to use this allow-list or a custom allow or deny list.

> ⚠️ Programmable NFTs and royalties rule sets are launching in beta. We expect the beta period to last 90 days, after which we’ll publish a stable set interfaces and features. Third-party audits of this new functionality are still ongoing, creators and developers should use at their own risk.
> 

## Upgrades for existing collections

> 📌 Migration of existing collections is completely optional. Creators who don’t want to migrate to `ProgrammableNonFungible` will remain on the existing `NonFungible` asset type.
> 

### Upgrade paths
Creators will have two upgrade paths for existing collections:
1. Timed upgrade initiated by the creator.
2. Community vote organized by the creator for collection holders.

The upgrade tool for existing collections will be available at [royalties.metaplex.com](http://royalties.metaplex.com) starting on January 6. Creators will need to connect the wallet that holds the update authority of their collection to check its eligibility and initiate the upgrade process. With both upgrade options there is a minimum 14-day notice period to holders, after which the creator will be able to complete the asset class upgrade. 
    
### Collection eligibility
Existing NFT collections will be eligible for the new asset class as long as:
1. The NFTs in the collection use Metaplex’s existing `NonFungible` standard with a master edition.
2. The NFTs in the collection are mutable. Immutable collections are not eligible for migration.
3. The freeze authority for the NFTs in the collection is held by the Token Metadata program.

### Upgrade window
Upgrading an existing `NonFungible` asset to a `ProgrammableNonFungible` one will be possible during 90 days, after which asset class migration will be closed.

After the 90-day upgrade window, creators will be able to choose to mint new assets using either the existing `NonFungible` standard or the new `ProgrammableNonFungible` asset class that supports royalties enforcement.

> 📣 We’re planning to iterate on Token Authorization Rules as it relates to royalties enforcement over the course of the 90-day upgrade window. We’ll keep engaging with creators, developers, and collectors to strike the balance between the flexibility programmable NFTs provide and predictability and transparency for buyers and holders. We consider programmable NFTs to be in beta until then.
> 

## Integration guide for developers

***Developers, marketplaces, wallets and utility programs that wish to support programmable NFTs will have to integrate with new instructions.*** We’ve put together a technical guide that includes a new set of unified instructions that will work across asset classes as well as details on each instruction + test code. 

[Programmable NFTs guide](https://github.com/metaplex-foundation/metaplex-program-library/blob/master/token-metadata/program/ProgrammableNFTGuide.md) | [Token Auth Rules program](https://github.com/metaplex-foundation/mpl-token-auth-rules/blob/main/README.md)

Feel free to leave your questions and comments directly on GitHub.

> 📌 New instructions will be backward compatible (i.e. work with `NonFungible` and `ProgrammableNonFungible` assets). Old instructions will keep working as usual to interact with `NonFungible` assets.
> 

## **Upgrade implications and risks**

### Tradeoffs between allowlists vs denylists
An allowlist-based configuration of Programmable NFTs, like the optional one maintained by the Metaplex Foundation, may break utility programs and other smart contracts that have not yet adopted the new instructions or have not yet been added to the list. This may cause your collectors to be frustrated in specific cases that will require you to respond. As recourse, you can always manually modify your collections allowlist to include programs on an as-needed basis to address these issues.

A denylist-based configuration of Programmable NFTs is easy to bypass since 0% royalty marketplaces can simply cycle program IDs, requiring an on-going and expensive cat and mouse game. However, this will be less restrictive and may be sufficient in creating the desired outcome which is to collect royalties in most cases.

### Utility program migration
If a utility program is not sending instructions to Token Metadata or SPL-Token (e.g. transfer or freeze), they will not need to make any changes to support Programmable NFTs.

Otherwise, if a utility program (e.g. staking) wants to mint, transfer, escrow, delegate, revoke, freeze, thaw or burn Programmable NFTs, it will need to call the new instructions in Token Metadata, as specified in the developer doc above.

### Immutable escrow-based programs

NFTs that are being held in immutable escrow-based programs may not be recoverable post-migration since they will not be able to update to new instructions. *Please communicate with your community that they should withdraw NFTs from immutable escrow-based programs ahead of the migration completing.*

### Reversibility

Royalty enforcement rule sets can be removed after a migration from `NonFungible` to `ProgrammableNonFungible.` This would make the Programmable NFT behave similarly to a standard NFT, but developers will still need to call the new instructions in Token Metadata. There are no plans to allow reverse migrations from `ProgrammableNonFungible` to `NonFungible`.

## Process to be included in optional rule set maintained by Metaplex Foundation

> 📣 This royalties rule set is optional and provided to creators for convenience. Creators will be able to create their own rule set based on an allow-list or a deny-list.
> 

Metaplex Foundation will be maintaining an optional rule set that provides royalties enforcement for convenience. We will be updating our optional royalties rule set on a weekly basis and will maintain a public list of programs included in the royalties rule set we maintain to ensure transparency for creators and collectors.

The requirements to be included in the royalties rule set maintained by Metaplex are as follows:
1. Your program needs to have integrated with Programmable NFTs 
2. Publicly tweet that one or more of your programs will pay creator royalties, including program addresses and tagging the [@metaplexstatus](https://twitter.com/metaplexstatus) account.
3. Provide sample transactions with comments on how your integration works. For marketplaces and other commerce programs this should cover how royalties are paid on-chain when NFTs are sold. 

## Built-in transaction layer for permission-less trading

Metaplex will provide a new, built-in transaction layer with shared liquidity so programmable NFTs can be traded by collectors, regardless of how a creator configures other rule sets. 

It will be open-source and free to use by any developer who integrates with it, addressing the concerns around hypothetical marketplace exclusivity deals and other barriers of entry for new developers.

This new program will be based on Auction House and only include the thinnest layer of features to enable NFT trading (i.e. only listings and bids — no AH instances, treasuries, configs). We will share more details about this new program as soon as possible by publishing a new MIP.

## Other considerations

- Interoperability with existing programs (e.g. staking contracts) is ensured by creator control over which programs may interact with the NFTs they create.
- Metaplex Program Library contracts will be updated to ensure compatibility with the new asset class before the end of the 90-day upgrade window (incl. Candy Machine, Auction House, etc.).
- Wallet-to-wallet transfers will not be subject to any restrictions to start. If these types of transfers are used as a way to circumvent royalties payments in the future, creators will have the option to add a wallet linking requirement in their rule sets by integrating with third-parties (e.g. Civic).
- We’ve considered the feedback we’ve received on providing creators with a royalties enforcement solution based on allow-lists and/or deny-lists and have decided on the following:
    - Creators will be able to create their own rule set and choose between an allow-list or a deny-list approach for royalties enforcement for their collections.
    - Metaplex’s optional royalties rule set will be based on an allow-list that we will maintain for convenience and will update every week. We believe that a solution based solely on a deny-list would not necessarily provide an adequate level of royalties enforcement. Creators and third-parties who wish to create a deny-list based rule set will be able to do so. We encourage a competitive ecosystem of third party rule sets addressing different needs over time that creators may choose from.
    - Based on usage, we’ll iterate to improve the way third-party managed rule sets work and are surfaced in our tools.
- Indexing of the new asset class will be ensured via Metaplex’s Read RPC extension used by wallets and RPC providers (already integrated by GenesysGo, Triton, Solflare, with Phantom, Alchemy, QuickNode coming in Q1 2023).

## Rollout schedule

1. ✅ Draft program interfaces available for public review [December]
2. ✅ Developer integration guide [on [GitHub](https://github.com/metaplex-foundation/metaplex-program-library/blob/feat/programmable-asset/token-metadata/program/ProgrammableNFTGuide.md)]
3. ✅ No-code migration tool for creators to start the upgrade process at [royalties.metaplex.com](http://royalties.metaplex.com) [Jan 6]
4. ✅ Devnet programs available for integration by marketplaces, wallets, dApps [Jan 12]
5. ✅ Beta launch of programmable NFTs with support for royalties enforcement. Functionality of asset class may change during this period based on feedback [Feb 6]
6. ✅ Candy Machine and Auction House support
7. 🗓 Built-in transaction layer with shared liquidity [date to be confirmed]
8. 🗓 Upgrade window for existing NFT collections closes [Apr 20]
9. 🗓 Programmable NFTs come out of beta [Apr 20]

## FAQs

**Which programs will be included in the optional royalties rule set maintained by the Metaplex Foundation?**
- Developers, marketplaces, wallets and utility programs that wish to support programmable NFTs will have to integrate with new instructions (see “Integration guide for developers” section). Please refer to the public requirements listed above if you’d like your program to be included.
- We will be working closely to ensure minimum viable programs (marketplaces and wallets) are compatible before the first creator can authorize their upgrade post 14 day notice period expiry.

**Do utility programs need to do any work to be compatible with programmable NFTs?**
- Utility programs that transfer, escrow, delegate, revoke or burn NFTs will need to update their instructions. We’ll share more details on how escrow-less utility programs can interact with Programmable NFTs is coming next week.
- Utility programs just checking for ownership or not interacting with token metadata do not need to use the new instructions.

**As a creator, can I add programs to my rule set even if they don’t honor royalties to ensure compatibility with my project?**

Yes, creators may add any programs they wish and trust to their own lists, even if they don’t honor royalties. Those programs will still need to integrate with the new instructions to be compatible with programmable NFTs.
    
**As a developer, am I required to use the new instructions?**

You will have to use the new instructions to interact with programmable NFTs. New instructions will be backward compatible (i.e. work with `NonFungible` and `ProgrammableNonFungible` assets). Old instructions will keep working as usual to interact with `NonFungible` assets.
    
**Will programmable NFTs be compatible with staking programs?**

Yes, however those programs will need to be updated to use our new instructions. Escrow-based programs will have to use the new transfer instruction and be allowed to interact with the collection by creators. We’ll share more details on how escrow-less utility programs can interact with Programmable NFTs next week.
    
**As a creator, am I responsible for maintaining my own rule set?**
- Creators will be able to enable royalties enforcement by creating their own rule sets that determine which programs may transfer their NFTs. If you create your own rule set, you will be solely responsible for maintaining it.
- The Metaplex Foundation will provide an optional rule set based on an allow-list that will be updated periodically to only include programs that pay creator royalties for convenience. Creators won’t have to do any extra work to benefit from those rule set updates.
- Based on usage, we’ll iterate to improve the way third-party managed rule sets work and are surfaced in our tools.

***

For older versions of this MIP and additional background information, please refer to [this commit history](https://github.com/metaplex-foundation/mip/commits/main/mip-1.md).
