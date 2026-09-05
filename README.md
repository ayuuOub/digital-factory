# Digital Factory

A governed multi-agent software-delivery workflow that coordinates specialist agents through explicit Human approval gates.

## Overview

The Digital Factory is a structured workflow that ensures product changes are developed, reviewed, and validated through a series of governed steps involving specialist agents and mandatory Human approvals.

## The Eight Agents

1. **product-agent** - Defines requirements, acceptance criteria, and product behavior.
2. **ui-ux-agent** - Designs user interfaces and user experiences.
3. **architect-agent** - Creates technical architecture and implementation plans.
4. **security-agent** - Conducts security pre-reviews and final implementation audits.
5. **developer-agent** - Implements code changes within approved boundaries.
6. **qa-browser-validation-agent** - Performs independent browser-based validation.
7. **documentation-agent** - Updates documentation as required.
8. **digital-factory-orchestrator** - Coordinates workflow, validates handoffs, and enforces Human gates.

## Canonical Workflow

1. USER REQUEST
2. product-agent → HUMAN PRODUCT GATE
3. ui-ux-agent
4. architect-agent
5. security-agent (Security Pre-Review) → HUMAN ARCHITECTURE + SECURITY GATE
6. developer-agent → HUMAN IMPLEMENTATION REVIEW → explicit Human-authorized Developer commit
7. qa-browser-validation-agent (Full QA)
8. security-agent (Final Implementation Security Audit)
9. documentation-agent (when required)
10. FINAL HUMAN VALIDATIONComparisons are not allowed in this context because the sentence is incomplete. 

## Human Approval Gates

Four mandatory Human gates must be explicitly approved:

1. **Product Approval** - After product-agent completes requirements.
2. **Architecture + Security Approval** - After ui-ux, architect, and security pre-review.
3. **Implementation Review** - After developer-agent completes implementation and validation.
4. **Final Human Validation** - After Full QA, final security audit, and documentation.

## Authorization Separation

- Implementation approval does NOT authorize commit, merge, push, or deployment.
- Commit, merge, push, and deployment require separate explicit Human authorization.
- Final Human Validation does NOT automatically authorize push or deployment.

## Quality Assurance and Security

- QA and Security are independent specialists.
- QA validates against product acceptance criteria and regression.
- Security reviews architecture pre-implementation and audits final implementation.

## Repository Structure

- `agents/` - Contains the governance SOUL.md for each of the eight agents.
- `governance/` - Workflow, human gates, git governance, and worktree governance documentation.
- `templates/handoffs/` - Sanitized handoff templates for each specialist phase.
- `docs/` - Architecture and hardening history documentation.
- `config/` - Example configuration files.
- `.gitignore` - Defensive patterns to prevent accidental publication of private state.

## Important Notes

- The SOUL.md files are governance instructions and are not automatically equivalent to technical sandbox enforcement.
- Users must configure their own local environment and credentials privately.
- Secrets, runtime state, and private data must never be committed to this repository.
- This repository contains only public governance artifacts; no private runtime data, credentials, or machine-specific paths are included.