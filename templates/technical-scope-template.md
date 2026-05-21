# General Technical Scope Template

> [!NOTE]
> ### General rules on **filling out** the template
> - No sections can be skipped or removed. If a section is non-applicable, provide a one-line explanation why it's not relevant.
> - All notes and warnings should be removed from the filled-in template before posting or submitting.
> - All addresses have to be in a checksummed format.

## Introduction

> [!NOTE]
> Contains enough context required for reviewing the doc by a complete outsider.

### Goal of this update

### Required context

### The reason(s) behind this update

### Timing of this update (in stages, if needed)

## Relevant audits

> [!NOTE]
> Optional section (due to the redundancy with the source code verification). Contains audits for the relevant contracts. Note: the audit report must be stored on the auditor's website to prove its authenticity; all links to the code in the document must always use an audited commit hash.

1. **[Audited repository]**
    - External URL to the audit report:
    - Exact commit at which the audit is concluded:
    - Relevant scope of the audit:
    - Diff with another independent audit, if any:

## Trusted addresses

> [!NOTE]
> Optional section (due to the redundancy with the source code verification). Contains a table with trusted sources used as a reference.

| **Contract name** | **Address with URL** | **Source URL** |
|---|---|---|
| | | |

## Pre-deployed contracts

> [!NOTE]
> List every contract that is deployed as a preparation for the planned infrastructure change. In scope is every contract that was created as a preparation for this update, internally or externally: proxies, as well as implementations, libraries, and multisigs, should all be listed here. In case a check has a non-blocking problem or a pending action, the problem as well as the reason why it's not a blocker has to be explicitly documented.

1. **[Contract name]**
    - Chain name:
    - Contract address (linked to the explorer):
    - Deployment transaction trace:
    - Deployment checklist: [publicly accessible link to the completed deployment checklist]
    - Code verification
        - If deployed by EOA
            - Source code URL (at the audited commit hash):
            - External URLs to the audit reports
            - Deployed bytecode is verifiable using `forge verify-bytecode` at the audited commit (or explanation of how the contract was verified otherwise).
            - Compilation optimizations match …, source ….
            - Constructor arguments:
                1. [Argument name]
                    - Argument value:
                    - External source of the value or an explanation of how this value can be verified, and who has to confirm it:
        - If deployed by a factory
            - Contract being called:
            - External docs page with this address:
            - Function being called:
            - Function arguments:
                1. [Argument name]
                    - Argument value:
                    - External source of the value or an explanation of how this value can be verified, and who has to confirm it:
    - Additional parameters configured on the contract by a privileged actor:
        1. [Reason behind this call]
            - Transaction trace URL:
            - Contract being called:
            - Function being called:
            - Function arguments:
                1. [Argument name]
                    - Argument value:
                    - External source of the value or an explanation of how this value can be verified, and who has to confirm it:
    - Ownership, roles, privilege callers:
        1. [Role name]
            - What actions can this role perform:
            - Address:
            - External source of the address or an explanation of how this address can be verified, and who has to confirm it:
    - Source code is verified on the block explorer:
    - The deployer no longer has a privileged role:

## Pre-configurations

> [!NOTE]
> List every additional action performed as a preparation for this change. For example, a deployer can sometimes be used to perform a configuration before passing the ownership of this contract/configuration to a proper "admin" contract.

1. **[Reason behind this call]**
    - Transaction trace URL:
    - Contract being called:
    - Function being called:
    - Function arguments:
        1. [Argument name]
            - Argument value:
            - External source of the value or an explanation of how this value can be verified, and who has to confirm it:

## Pre-requirements

> [!NOTE]
> List every additional prerequisite for performing the planned action. This section should be used to outline *external* dependencies or not-yet-performed actions. For example, it can include a requirement for a core spell to adjust rate limits, whitelist SubProxy, etc. It can also require an operator to queue an emergency transaction and, at the same time, outline a dependency for the planned action on a legal approval or an audit. Once the pre-requirement is satisfied, the draft can be edited to specify a proof.

1. **[What needs to be done]**
    - Intended end goal:
    - Why is it required to be done in advance:
    - Proof that it was done or planned to be done:

## Proposed actions

> [!NOTE]
> List every action planned to be performed after the pre-requirements are satisfied. In case of spells, this section should contain recommended spell instructions. In case of vault deployments, it should contain scripts (at the exact commit hash) that are planned to be executed with exact input values and their sources, as well as the exact address that will perform those actions. In case the actions are planned to be performed by a multisig, this section should link already staged transactions.

1. **[What is proposed]**
    - Business reason behind this action:
    - Who will perform this action:
    - Important arguments:
        1. [Argument name]
            - Argument value:
            - External source of the value or an explanation of how this value can be verified, and who has to confirm it:

## Post-checks

> [!NOTE]
> List every check planned to be performed to verify the liveliness of the system after the execution of the proposed actions. E.g., in case a new module is launched, test transactions should be performed in order to confirm that the module is operational.

1. **[Reason]**
    - What will be done:
    - How it will be done:
    - Expected outcome:
    - Who will perform this action:

## Technical risk self-assessment

> [!WARNING]
> **SECURITY-SENSITIVE — DO NOT POST this section to the Forum. For private submission only.**

> [!NOTE]
> Outline the highest value that can be lost due to the basic misconfiguration, frontrunning risk, or undiscovered vulnerability in the new module, onboarded protocol, etc. List each risk as a separate point, together with its known mitigation or accumulated lindy.

1. **[Risk description]**
    - Applied mitigations:
    - If relevant, known lindy:
        1. [Name of this deployment]
            - Historical TVL:
            - Source of the TVL:
            - Link to the explorer:

## Emergency actions

> [!WARNING]
> **SECURITY-SENSITIVE — DO NOT POST this section to the Forum. For private submission only.**

> [!NOTE]
> List every relevant emergency action that can mitigate incorrectly performed infrastructure changes. For example, a link to the freezer with a staged transaction.

1. **[What can be done]**
    - When to do:
    - How to do it:
    - Known side-effects:
    - Is covered by monitoring:

## Monitoring

> [!WARNING]
> **SECURITY-SENSITIVE — DO NOT POST this section to the Forum. For private submission only.**

> [!NOTE]
> List every monitoring that was set up internally or by the external team.

1. **[Invariant/What is being monitored]**
    - How it is being monitored:
    - By which team:
    - What happens when the invariant is breached:
    - Relevant emergency actions:

## Research and additional notes

> [!NOTE]
> An optional section that contains any work that was done to come up with the content of other sections. The goal is to keep other sections as minimal as possible, containing only the information that other technical teams have to verify. For example, it can contain additional checks that were performed, scripts that were used, thought process behind proposed actions. Teams performing an *independent* review of the document don't have to review the content of this section.
