# [MIP-2][WIP] Programmable Tokens

Created time: November 18, 2022 11:30 AM
Status: Draft

# Summary

Solana has seen rapid growth in the number of NFT minted over the last 12 months with the most popular use case being the Profile Picture (PFP) NFTs. Many utility use cases have developed over time, led by forward thinking projects and games however as a result, there has been a fragmentation and stagnation in the types of on-chain utility possible due to the ecosystem adoption challenges.

To address these challenges, Metaplex introduces a new set of `Programmable` tokens (fungible, semi-fungible and non-fungible) to both standardize how behaviors are represented/discovered and to provide a framework for creators and developers to easily create custom on-chain behaviors for their NFT collections. The behaviors are modeled as `RuleSets` that are applied to each lifecycle event or `Action` that can be defined at creation time by the creator or developer. Metaplex will provide a standard library of rule sets and rules developers may take off the shelf in addition to any custom rules or rule sets they wish to write or use.

This is the first step towards the Digital Asset Standard vision Metaplex published in early 2022 which also included other concepts such as schemas, modules, extensions and standards.

# Terminology

### Asset Class

An asset class, represented in code as the`TokenStandard` is the highest order, on-chain representation of a digital asset’s set of behaviors: `Actions`. 

### Actions

Also known as Life Cycle Events. These are the methods/instructions that are allowed to be invoked on an NFT. Common actions are:

- Create
- Burn
- Update
- Transfer
- Delegate
- Revoke

Different asset classes may have different `Actions` that are available to them.

### Delegate roles

The `Delegate` action has roles which represent the current owner’s intent when delegating a token. Rules may be applied based on the delegate role in order to provide different behaviors.
These allow delegation of rights. 

Example Delegate Roles:

Collection -> can manage items to a collection
Use -> can use the token on behalf of a owner
Sale -> can trade the token on behalf of the owner 
Utility -> can freeze, thaw and transfer the token under certain circumstandes
MetadataAuthority -> can change metadata


### RuleSet

A rule set is a collection of `Rules` that may be applied to an `Action` when it is invoked. If all the rules in a rule set are met, the action can be executed. Currently, only one rule set can be specified per NFT or collection at any one time.

### Rule

A executable function that returns a boolean value. More sophisticated rules can look at the result of on chain oracles or prior instructions in the transaction for custom behavior.

### Schema

The schema describes the shape of the off chain JSON schema. While schemas (e.g. audio NFT) are orthogonal to a token’s behavior, schemas may be used in the future for as convenience to describe complex NFT behaviors.

# Programmable tokens

This proposal adds three new asset classes to the `token-metadata` program:

1. `ProgrammableNonFungible`
2. `ProgrammableFungible`
3. `ProgrammableFungibleAsset` also known as programmable semi-fungible

All three asset classes function in the same way with respect to `Actions`, `RuleSets` and `Rules`.

In addition to the existing metadata fields for each of the respective existing asset classes, the `Programmable` asset classes adds the following structures:

```rust
// psuedo code
pub struct Metadata {
	// ... existing fields
  pub token_standard: Option<TokenStandard>, // Should be one of the Programmable asset classes
  // ...

  // Programmable config
  pub programmable_details: Option<ProgrammableDetails>,
}

pub struct ProgrammableDetails {
  pub rule_set: Pubkey,
}

pub struct RuleSet {
  pub rules: Vec<Pubkey>,
}

pub struct Rule {
  pub action: Action,
  pub rule_type: RuleType,
  pub fee: Option<u64>, // Devs may specify fees for their custom rules if others use them
}

pub enum RuleType {
  ValidateBoolean { args }, // args could be static (e.g. oracle result addr), or passed in
  ValidateEquals { args },
  TriggerExtension {args },
  Dsl { args },
	// more
}

pub enum Action {
  Mint,
  Burn,
  Transfer,
  Delegate,
  Undelegate,
}
```

# Rule sets

### Base rule sets

Metaplex will provide some basic ready to use rule sets for common use cases such as royalty enforcement or non-transferrable (soulbound) tokens. This library will grow over time as common use cases arise.

Metaplex will also provide a set of basic rule primitives that may be composed to achieve more sophisticated rule sets. The list is as follows:

- Validate an account value with standard comparators: =, <, >, ≥, ≤, ≠
- Validate an account address with standard set comparators: in, not in a list
- more…

### Advanced rule set patterns

Since CPI’ing from a rule into a 3rd party program can introduce a lot of complexity as well as security issues, in order to use custom code for validation, the following patterns are available:

1. A rule can be written to check a specific account that is written to by an oracle
2. A rule can be written to inspect the results of instructions in the same transaction
3. CPI may be available in the future however the functionality would be restricted to some sort of DSL.

### 3rd party/custom rule sets

Any developer or creator can create their own rule set and rules and create tokens that use those custom rules. Custom rule sets may also use any combination of rules provided by Metaplex’s rule library and rules written by any community developer.

### Rule set registry

Developers may decide that the custom rules and rule sets they’ve developed would be valuable to the community and would like to monetize them. Metaplex would welcome a registry of popular or useful rules that the developer community could use off the shelf to build new experiences.

# Actions

### Custom or derivative actions

TODO

### Action extensions

Often programs need to execute code when an action or lifecycle event happens to a token. The current way to do this is to wrap the token completely and force all instructions to via the program that wraps the token. Programmable tokens provides a lightweight alternative that allows on chain programs to be triggered by actions that occur on a token, such as transfers.

# Instructions

- interaction versioned, with rule sets
- spl-token proxy

# Indexing

- JSON descriptors
- Read API


# Example new use cases
TODO

# Future

- Extensions write backs
- extensions, oracles run by metaplex or 3rd parties
- compression
- cpi dsl
- custom actions
- delegate workflow


