# [MIP-10] Optional deterministic cNFT asset IDs

[Submission details](https://github.com/metaplex-foundation/mip/discussions/40)

# Overview
In the current cNFT minting solution there is no way to determine a cNFT Asset ID before the cNFT Mint transaction is processed on-chain. Here are a two examples when this is limiting or inconvenient:

- The AssetID is needed to construct a follow up on-chain call. This can be the case for example when using the Asset ID to deterministically construct a PDA tied to the underlying cNFT (e.g. with Access Protocol Transferable subscriptions). If there was a way to determine the Asset ID in advance these two calls could be merged into a single transaction or even into a single instruction utilising CPI calls.
- cNFT mint monitoring - To be able to store the Asset ID in a database for a later use (e.g. DAS API calls) a non-trivial asynchronous logic is required. Additional RPC call (or Other solution like Geyser plugin) and non-trivial transaction parsing is needed to retrieve the Asset ID.

# Current implementation
Currently the Asset ID is derived from the Merkle address and number of minted assets (num_minted) stored in the Tree Config PDA owned by the Bubblegum program. The num_minted is then used as the leaf index in a CPI call to compression program to set up a new leaf in the Merkle tree. Finally, the value of num_minted is increased by 1. This ensures that the mint instruction never fails if the tree is not full.

# Proposed solution
After thorough examination of the current Bubblegum code I've come up with a following plan of possible mitigation of the aforementioned issue:

- To keep the backwards compatibility this should be implemented as a separate instruction that would accept the Asset index as a parameter. This would be used for determining the leaf index instead of current num_minted value
- The instruction should either require the Asset index to be equal to num_minted for a backwards compatibility with existing trees, or only be available on dedicated trees that could be filled in non-deterministic order.
- Other than this change, the instruction logic would be exactly the same as the existing Mint instruction.

