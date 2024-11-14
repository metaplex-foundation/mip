# [MIP-7] Edition Print Authorities

[Submission details](https://github.com/metaplex-foundation/mip/discussions/28)

# Overview

The Token Metadata program currently only supports printing editions from a master edition if the signer is also the owner of the token. This forces creators to escrow their master edition token when listing an edition sale on a marketplace, as the marketplace must be the owner of the token in order to print editions. This also prevents the creator from being able to list their master edition to be printed on multiple marketplaces concurrently.

# Motivation

The main motivation behind the proposal to add edition print authorities is to give creators the ability to list edition sales on multiple marketplaces concurrently. This gives creators more flexibility in how they choose to sell their work while remaining in control of their master edition. Marketplaces will also benefit from this feature as creators would no longer be forced to choose a single marketplace to list their work on.

# Proposal

It is our proposal to add a new PrintAuthority authority type, similar to how CollectionAuthority works, along with the instructions to approve and revoke authorities. A new print_v2 instruction would also be required to print an edition using a verified print authority.



