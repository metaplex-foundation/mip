# [MIP-3] Sized Collection Feature Deprecation

# Overview

Sized Collections, which were introduced in [version 1.3](https://docs.metaplex.com/programs/token-metadata/changelog/v1.3) of Token Metadata, track the size of an NFT collection by calculating collection size change based on the lifecycle events (creation and destruction) of all NFTs in the collection and storing the calculated size in a struct on the collection NFT. This feature was initially introduced to solve use cases such as DAO voting based on NFT collection ownership. Significant time has passed since this feature was launched and we’ve learned about its usage and uncovered various consistency issues that negate the feature’s intended purpose.

As such, this proposal is to facilitate discussion of deprecation and removal of this feature from Token Metadata. The reasoning behind deprecation is outlined in detail in the sections below. Please see this GitHub discussion to weigh in with thoughts on this proposal along with the associated reasoning.

# Motivation

There are several motivations behind this proposal:

1. **Inherent unreliability of the Sized Collection counting logic**
2. Reduction of binary space in the Token Metadata program
3. Simplification of the Token Metadata instruction logic

Token Metadata is at its binary size limit and removal of rarely used features will help facilitate further development. Sized Collections are also a relatively complex feature that requires additional verification, accounts, and calculation steps to be performed in all situations where an NFT can be added or removed.  Removal of this feature would reduce the amount of validation that needs to be done in those instructions and would result in one less account (The Collection NFT) in instructions that burn NFTs. Lastly, as outlined below the feature and the Collection Size is unreliable under the current architecture of Solana NFTs.

## Edge Cases in Size Calculation

There currently exist various edge cases where Collection sizes can be incorrect, through either bugs or NFT lifecycle paths that don’t include Token Metadata in the loop.

### Partial Burn of NFTs/FAs (Fungible Assets) in a Collection

Standard NFTs and Fungibles assets operate as extensions built on top of the SPL-Token program. All lifecycle events of the token itself are handled by the SPL-Token program making it impossible to reliable track them at the Token Metadata level. While Token Metadata has an instruction which performs a burn of both metadata and the token, which can therefore decrement the collection size, holders often burn using the simpler SPL-Token burn instruction, therefore bypassing the decrementing of the collection size. Oftentimes the size of the collection is higher than the actual number of tokens.

Note that this restriction is not the case for pNFTs which control the full set of token lifecycle events and therefore can reliably track collection size.

### Burn of Fungible Assets in a Collection

Currently there is a bug in Fungible Assets where the collection size is incremented/decremented by 1 even for a token supply greater than 1. This can result in a situation where FAs are added or burned from a collection in quantities, vastly deviating the collection size from the proper value. Additionally, Token Metadata is not the mint authority on FAs and so tokens can be minted without including Token Metadata in the loop to properly track the size of the collection.

### Inconsistent addition of Editions to Collections

The current Print functionality of NFT Editions involves including printed editions in the Master NFT’s collection, but not incrementing the collection size. However, Editions added to a collection manually using the Verify command will increment the collection size.

## Difficulty in Measuring Feature Utilization

Sized Collections is a feature that is included by default in creation with a corresponding collection verification and burn instructions during the lifecycle of the NFT. The actual size also requires no on-chain operations to read. Therefore it is very difficult to measure the actual usage of this field. Currently the only way to determine its frequency of usage is through manual communication avenues such as Twitter and this RFC process.

## Pros of Removal

- Reduction of size of Token Metadata
- Simplification of burn, verify, and unverify instructions and removal of their sized variants.
- Removal of one account from the burn instructions

## Cons of Removal

- No longer an on-chain way to determine collection size

# Proposal

It is Metaplex’s proposal that the Sized Collection feature of NFTs be deprecated and eventually removed from Token Metadata in order to reduce complexity and remove a feature that does not work in a consistent enough fashion to serve its purpose. It is our assumption that the benefits of removing it are more applicable to all users and therefore outweigh the downsides.

If this assumption is discovered as incorrect, it is our recommendation that Sized Collections be limited to pNFTs as the only standard that can accurately track collection size.

## `CollectionDetails` Replacement Options

In the case of Sized Collections deprecation, there are several possible options for changes that can be made to the data structure in the on-chain metadata. These options are listed out with an explanation and pros and cons below.

**Removal** - This would entail completely removing the struct to reclaim space, but would have negative consequences of no longer being able to easily tell if an NFT is a collection NFT.

**Leave it alone** - In this case the field would be completely untouched, but this has the potential to confuse new users by having a zero value for Collection Size.

**Empty Struct (Recommended)** - The struct could be left in place but the collection size field could be removed. This would reclaim eight bytes of data and leave the ability to detect if the NFT is a collection NFT. This also leaves in the possibility of adding more details to the Collection Details struct in the future.

## Alternative Solutions

- When measurement of a mint amount is required, create a small on-chain program that is is executed alongside mint and counts the number of mints.
- Create a Collection Size Oracle that writes collection size on chain from data retrieved from indexers such as Helius, Shyft, or any DAS API implementors.

# Community Asks

- How is your project using the sized collection feature?
- How would this proposal affect your project?
- What other technical alternatives should the Metaplex Foundation consider?
- What technical implementation constraints does your project have relating to the sized collection feature?
- Any other pertinent input?

# Discussion
https://github.com/metaplex-foundation/mip/discussions/6

# Decision

After soliciting community feedback, the usage of Sized Collections for NFTs has been found to be minimal. The primary use cases are related to collection governance, which is not reliable due to the caveats outlined below. As such the proposal to remove Sized Collection is approved and the feature will be deprecated and eventually removed from the Token Metadata program.

## Unreliability as a Governance Mechanic

Sized Collections have been utilized to provide a voting mechanism to establish the weight that each NFT in the collection should have when voting on proposals. However, there is no reason why this mechanism would be any more reliable than setting the vote weight manually on the SPL-Governance instance. A creator who holds update authority over the collection and collection NFT has permission to add or remove from a collection at will. This means that NFT vote weight can be swayed arbitrarily by a malicious creator. Additionally, the collection field lies outside of the data struct and is therefore not covered by immutability. This allows a creator to modify collection sizes even on immutable NFTs.

Having collection size be set manually in the governance instance, or even set via governance proposal, is a more reliable method of assuring proper NFT vote weight than using Sized Collections.
