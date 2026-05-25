# Morpho Deployment Verification Guide

## Summary

This document defines a repeatable approach for validating Morpho vault deployments and market configuration, then applies that approach to the specific in-scope deployments as a worked example. The verification flow covers canonical Morpho infrastructure, factory deployment provenance, market and oracle parameters, vault roles, timelock settings, and audit coverage.


## Scope
Objective: define verification boundaries and primary data sources used throughout this document.

## General Morpho Vault / Market Verification Methodology

Use this process to verify a Morpho deployment before treating vaults or markets as production-valid.

### 1. Establish Scope

Collect the expected deployment inventory:

- Morpho core protocol address
- Vault factory address
- Oracle factory address
- Adapter factory address
- Registry address
- IRM address
- Vault addresses
- Market IDs
- Morpho oracle addresses
- Feed oracle addresses
- Adapter addresses
- Role assignments
- Timelock values
- Collateral, loan asset, LLTV, IRM, oracle, and feed parameters for each market

### 2. Verify Canonical Morpho Infrastructure

For each canonical Morpho contract, compare the address against Morpho’s official address documentation.

Expected evidence:

- Official Morpho docs link
- Chain/network
- Contract name
- Address
- Result

### 3. Verify Vault / Oracle / Adapter Deployment Provenance

For each deployment-specific contract, confirm that it was created by the expected Morpho factory. Also require independent Lindy corroboration of that factory address: verify it has deployed multiple live contracts and that a subset of those contracts (e.g., oracles/vaults) is discoverable in the official Morpho app, reducing reliance on docs alone.

Check:

- Contract creation transaction on Etherscan or equivalent explorer
- Factory address that emitted or executed the deployment
- Created contract address
- Constructor/init parameters where available
- Any bundler or intermediary caller, if applicable

Pass condition:

- The deployed address matches scope
- The creation path traces back to the expected Morpho factory

### 4. Verify Market Parameters

For each market ID, verify the live market configuration against the expected scope.

Check:

- Collateral asset
- Loan asset
- LLTV
- IRM
- Oracle
- Oracle feeds
- Market ID
- Chain/network

Preferred sources:

- Morpho app market page
- Morpho API
- Direct on-chain calls where available

Pass condition:

- Live market parameters exactly match the documented expected parameters
- Oracle values cross-checked against DefiLlama prices via Morpho [oracle decoder](https://oracles.morpho.dev/oracle-decoder)

### 5. Verify Oracle Configuration

For each oracle, verify the configuration path used to price collateral versus loan asset.

Check:

- Base asset path
- Quote asset path
- Chainlink feed addresses
- ERC4626 conversion paths, if applicable
- Feed decimals / scaling assumptions
- Whether any feed is intentionally absent

Pass condition:

- Oracle configuration matches the expected market design
- Missing feeds are explained by the intended oracle path, not left ambiguous

### 6. Verify Vault Roles and Timelocks

For each vault, verify governance and operational permissions.

Check:

- Owner
- Curator
- Sentinel
- Allocator
- Guardian / other role holders, if applicable
- Timelock duration per sensitive action

Pass condition:

- Live role assignments match scope
- Timelock values match the intended governance policy
- Standard Morpho timelocks (required for Morpho UI listing) confirmed via [vault listing](https://listing.morpho.dev/vaults-v2)

### 7. Verify Audit Coverage and Provenance

Check Morpho’s published audit index and available reports.

Record:

- Relevant audits
- Covered components
- Report availability
- Whether deployed bytecode can be mapped to audited source
- Any commit/tag traceability gaps

Pass condition:

- Audit coverage is documented
- Any source-to-bytecode uncertainty is explicitly disclosed

### 8. Record Results in an Evidence Matrix

For each checked item, record:

- Scope reference
- Contract or market
- Expected value
- Live value / evidence source
- Result
- Notes


## Sky Morpho Deployment Verification Results
Objective: verify section 3 contract addresses and deployment provenance against Morpho docs and factory creation evidence.

| Section | Vault | Contract Type | Contract Address | Expected Source / Factory | Evidence (Doc or Tx) | Result | Notes |
|---|---|---|---|---|---|---|---|
| 3.1 | - | Morpho | `0xBBBBBbbBBb9cC5e90e3b3Af64bdAF62C37EEFFCb` | Morpho docs | [docs](https://docs.morpho.org/get-started/resources/addresses) | PASS | ok |
| 3.1 | - | MorphoChainlinkOracleV2Factory | `0x3A7bB36Ee3f3eE32A60e9f2b33c1e5f2E83ad766` | Morpho docs | [docs](https://docs.morpho.org/get-started/resources/addresses) | PASS | ok |
| 3.1 | - | VaultV2Factory | `0xA1D94F746dEfa1928926b84fB2596c06926C0405` | Morpho docs | [docs](https://docs.morpho.org/get-started/resources/addresses) | PASS | ok |
| 3.1 | - | MorphoMarketV1AdapterV2Factory | `0x32BB1c0D48D8b1B3363e86eeB9A0300BAd61ccc1` | Morpho docs | [docs](https://docs.morpho.org/get-started/resources/addresses) | PASS | ok |
| 3.1 | - | MorphoRegistry | `0x3696c5eAe4a7Ffd04Ea163564571E9CD8Ed9364e` | Morpho docs | [docs](https://docs.morpho.org/get-started/resources/addresses) | PASS | ok |
| 3.1 | - | Adaptive Curve Irm | `0x870aC11D48B15DB9a138Cf899d20F13F79Ba00BC` | Morpho docs | [docs](https://docs.morpho.org/get-started/resources/addresses) | PASS | ok |

## Morpho Audit Coverage Verification

### Objective
Assess whether the Morpho contracts used by these deployments were audited by trusted external third parties, and whether the audited source can be confidently mapped to deployed contracts.

### Source
- Morpho audit index: https://docs.morpho.org/get-started/resources/audits/

### Findings
- Morpho documentation provides an audit guideline/index and lists multiple audits.
- Full underlying audit reports are not consistently available from all audit providers.
- In this review, full reports were directly obtainable only for Spearbit/Cantina items.

### Verification Gaps / Red Flags
- Morpho docs do not clearly identify the exact commit/tag used for deploying the relevant factory contracts.
- Without that provenance, bytecode-to-audit-source mapping cannot be conclusively verified from public artifacts alone.
- The main branch has advanced with many commits after published audits, which weakens confidence in direct linkage between audited source and currently deployed code.

### Counterpoint (Operational Evidence)
- The factory and related contracts have been live for months and are heavily used.
- No major incidents were identified during this verification process.
- This provides practical Lindy-style confidence, but it is not a substitute for strict source-to-bytecode audit traceability.
