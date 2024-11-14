# [MIP-9] cNFTs Composability Improvements

[Submission details](https://github.com/metaplex-foundation/mip/discussions/33)

# Overview

cNFTs have an extraordinary potential. However, like every technology that exists, their application also has a dark side. They have enabled bad actors to send malicious spam NFTs at a rate that overwhelms current users and actively deters new users.

They are able to be created in such a way that can break transactions, causing platforms to have to implement extensive workarounds to let them be burnt.

Additionally, these transaction breaking configurations prevent seamless composability across other types of platforms as well.

# Motivation
The main motivation behind the proposal is to fix the ability to create transaction breaking cNFTs, which appears to be a bug and not a feature.

If enacted, burns of these specific scam cNFTs can resume as any other cNFT, reducing the friction required to dispose of them.

In addition this would increase the composability of cNFTs across various applications and platforms within the ecosystem, not just limited to burning.

# Proposal
Set limitations on combinations of max depth and canopy depth to limit max size of proof bytes required to a lower limit than currently.

This could be simply enough to just permit all bubblegum instructions to complete, such as burn and transfer, but ideally, it would leave some space free to permit some amount of composability with other programs.

Looking at the costs and proof sizes on https://compressed.app/advanced, I believe permitting a maximum of 17 additional proofs should be sufficient, while still allowing people to mint a lot of cNFTs for a low cost.

For example, a max depth of 18, and a canopy depth of 1 would be permitted - the total proofs equals 17
A max depth of 30 would require a canopy depth of at least 13
A max depth of 24 would require a canopy depth of at least 7

# Potential Downsides

Although this would not limit the ability to manage an extreme amount of cNFTs with one tree, it would make certain configurations slightly more expensive.
