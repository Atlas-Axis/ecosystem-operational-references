# Ecosystem Operational References

Canonical operational reference materials for teams preparing, reviewing, and executing infrastructure changes and deployments within the Sky Ecosystem. These materials are used by Agents, Core Spell Teams, and other ecosystem participants as applicable.

This repository is intended to operationalize the relevant Atlas requirements and processes. Direct Atlas references will be added once the associated Atlas edits are finalized.

**Note:** The Agent Spell Reviewer Checklist currently remains maintained in its existing canonical location here: https://github.com/sky-ecosystem/pe-checklists/blob/master/spell/star-spell-reviewer-checklist.md. Agents and reviewers should continue using that version until further alignment on repository structure and migration decisions is completed.

## Contents

```
ecosystem-operational-references/
├── templates/
│   └── technical-scope-template.md
├── checklists/
│   └── deployment-checklist.md
├── examples/
│   └── technical-scope/
│       ├── star-spell-technical-scope-example.md
│       └── non-spell-technical-scope-example.md
├── .claude/skills/
│   └── submit-technical-scope/  ← guided submission skill
│   └── submit-technical-scope/  ← guided submission skill
└── .github/workflows/       ← placeholder for future workflows
```

## Guide

### Technical Scope Template (`templates/technical-scope-template.md`)

**What it is:** A standardized template for announcing any infrastructure changes (on- or offchain) with enough technical detail for an external team to review without additional context.

**Security-sensitive sections:** The template introduces sections for Technical risk self-assessment, Emergency actions, and Monitoring. These sections enforce a rigorous security mindset by requiring teams to consider risks, emergency responses, and monitoring for every infrastructure change. Because these sections may contain information that could be exploited if publicly disclosed, they are handled through a separate private submission process.

**Where to submit:** The filled-in template must be submitted through both public and private channels:

- **Public:** All sections except the security-sensitive sections defined above must be published as a Forum post on the Sky Forum.
- **Private:** The full template, including the security-sensitive sections (Technical Risk Self-Assessment, Emergency Actions, and Monitoring), must be submitted as a Pull Request in your Agent's private submissions repository. Atlas Axis must approve before the submission can be merged.

**How to submit:**

a) **Manually:** Pull the latest version of this repo, copy the template, fill it in, and submit the completed document as a PR in your Agent's private submissions repository. See the [Getting started](#getting-started) section below.

b) **Using the Claude skill:** Run `/submit-technical-scope` in Claude Code from this repo. The skill copies the latest template, opens it for editing, runs a pre-submission review when you're done, and handles the PR submission.

**For Agents:** For Technical Scopes associated with a Prime Spell, both the Forum post and the private submission must be completed according to the following deadlines:

- **Sky Governance path** (Prime Agents whose Root Edit Primitive is not yet operational): by **Wednesday, 16:00 UTC of Week 1** of the Prime Spell Process.
- **Independent Governance path** (Prime Agents whose Root Edit Primitive is operational): by **end of Friday of Week 1** of the Prime Spell Process.

### Deployment Checklist (`checklists/deployment-checklist.md`)

**What it is:** A standardized checklist for contract deployments covering deployer hygiene, foundry setup, test deployments, and verification.

**When to use:** For every contract deployment within the Sky Ecosystem.

**Where to submit:** The completed checklist must be attached to the deployment script Pull Request or, if no Pull Request exists, documented in a GitHub issue within the repository of the deployed code.

## Getting started

Clone this repository:

```bash
git clone https://github.com/Atlas-Axis/ecosystem-operational-references.git
```

## Before you start

> [!IMPORTANT]
> Before using any reference material, you must pull the latest version to ensure your copy is aligned with the source repository:
> ```bash
> cd ecosystem-operational-references
> git pull origin main
> ```

Do not modify the template files directly. When filling out a template, copy it to a new file with a descriptive name (e.g., `technical-scope-may-2026-spell.md`) and work from the copy. This ensures `git pull` always updates the templates cleanly without merge conflicts.

Each template and checklist must be completed and submitted separately, in accordance with the submission instructions in this README and any guidance within the documents themselves regarding which sections need to be filled out.

## Maintenance

### Technical Scope Template

The Technical Scope Template is maintained by Core GovOps. All changes must be submitted as a Pull Request in this repository and require two (2) approvals, one (1) from each Core Spell Team, before they can be merged.

### Deployment Checklist

The Deployment Checklist is maintained by Core GovOps. All changes must be submitted as a Pull Request in this repository and require two (2) approvals, one (1) from each Core Spell Team, before they can be merged.
