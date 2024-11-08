# [MIP-8] Soulbound NFTs

[Submission details](https://github.com/metaplex-foundation/mip/discussions/30)

# Introduction

This MIP seeks to move the wallet-to-wallet check to Token Auth Rules as an optional rule. The "wallet-to-wallet check" in Metaplex's token authorization rules is a specific condition governing token transfers between wallets. This potential change introduces additional flexibility and use cases to Non-Transferable "Soulbound" Programmable NFTs (pNFTs) for the Solana ecosystem.

Soulbound pNFTs offer a new dimension of digital ownership, enabling innovative applications by building atop Metaplex's Token Metadata program, which supports the Token 2022 Non-Transferable Tokens extension. By enabling more flexibility of Soulbound pNFTs via the wallet-to-wallet check, we can unlock unique use cases and provide creators with more tools regarding the non-transferable digital assets they create.

# Summary
The primary objective of this MIP is to "Enable Soulbound pNFTs by moving wallet-to-wallet check to Token Auth Rules as an optional rule." Implementing Soulbound pNFTs, which are non-transferable by design, will unlock new pNFT use cases such as:

- Event Tickets: Non-transferable tickets to exclusive events.
- Certifications: Proof of achievements or qualifications.
- Membership Tokens: Access tokens for exclusive clubs or services.
- Badges: Recognition of accomplishments or participation.
- Credentials: Verification of identity or qualifications.
- Onchain Identity Tokens: Permanent markers of digital identity.
- Game Inventory: Account-bound in-game assets or items.
- Personal Ledger: Record book of milestones, achievements, and stats.

# Motivation

- Innovative Use Cases: Soulbound pNFTs pave the way for new pNFT use cases, such as non-transferable badges, credentials, etc.
- Digital Scarcity and Exclusivity: Soulbound pNFTs introduce a new layer of digital scarcity, making certain assets unique and non-transferable.
- Enhanced Security: By limiting transfers, soulbound pNFTs can reduce the risk of unauthorized sales or transfers.
- Empowering Creators: This feature allows creators to dictate the terms of ownership, ensuring their vision for the pNFT is maintained.
- Onchain Identity: Soulbound pNFTs can serve as the foundation for persistent on-chain identity and reputation systems.

# Specifications
- Soulbound Auth Rule: Introduce a new authorization rule for Soulbound pNFTs, restricting all transfers post-mint by moving the wallet-to-wallet check to Token Auth Rules.
- Minting Process: Allow creators to designate pNFTs as "Soulbound" during minting, which will automatically apply the Soulbound auth rule.
- Loss Mitigation: Explore mechanisms to permit transfers to another wallet held by the owner of the original wallet in which the Soulbound pNFT was sent in scenarios like wallet migrations or loss recovery. For example, Metaplex could and should also prioritize allowing third-party authorization rules so identity standards can be added for loss mitigation.
- Transparency and Verifiability: Ensure that the Soulbound property of a pNFT is transparently visible and identifiable on-chain. While all interactions with the pNFT, including its Soulbound status changes, are recorded as transactions, it's crucial that the non-transferable nature of Soulbound pNFTs is easily distinguishable and verifiable on the Solana blockchain.
- Soulbound pNFT Burnability: Soulbound pNFTs should be burnable to allow owners to thwart bad actors who may send Soulbound pNFTs deemed inappropriate (NSFW, offensive, etc). Due to the irreversible act of burning pNFTs, in case of accidental burn by an owner, creators can opt to reissue a burned Soulbound pNFT or decide against re-issuance based on their policies.

# Proposal

Move wallet-to-wallet check to Token Auth Rules as an optional rule.










