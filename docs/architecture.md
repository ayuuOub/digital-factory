# Digital Factory Governance Architecture

This document describes the governance architecture of the Digital Factory multi-agent software-delivery workflow.

## Core Components

### Human
The Human provides explicit approval at mandatory gates and authorizes specific operations (commit, merge, push, deployment). The Human is the ultimate authority for progression between major workflow phases and for protected operations.

### Digital Factory Orchestrator
The Orchestrator coordinates the workflow, maintains state via Hermes Kanban, validates handoffs, enforces Human gates, and routes corrections. The Orchestrator does not implement product code or impersonate any specialist agent.

### Specialist Agents
Seven independent specialist agents operate within clearly defined responsibility boundaries:
1. **product-agent** - Defines WHAT must be built (requirements, acceptance criteria)
2. **ui-ux-agent** - Designs user interfaces and experiences
3. **architect-agent** - Creates technical architecture and implementation plans
4. **security-agent** - Conducts security pre-reviews and final implementation audits
5. **developer-agent** - Implements code changes within authorized workspace
6. **qa-browser-validation-agent** - Performs independent browser-based validation
7. **documentation-agent** - Updates documentation as required

Each agent:
- Receives approved inputs from previous phases
- Produces verifiable evidence of their work
- Operates only within their assigned worktree
- Does not expand scope or impersonate other agents
- Stops work for Human approval when required by the workflow

## Routing Model

The Orchestrator uses Hermes Kanban as the primary workflow control plane:
- Creates specialist tasks with explicit assignees
- Establishes parent/child dependencies when appropriate
- Preserves traceability from request to final validation
- Does not rely on automatic decomposition (auto_decompose = false)
- Creates only the task required for the current governed phase
- Waits for Human gate approval before proceeding to dependent phases

## Specialist Independence

Each specialist agent is independent in their execution:
- Product-agent decides product scope and acceptance criteria
- UI/UX-agent decides interaction design and visual hierarchy within product scope
- Architect-agent decides technical design and component boundaries within product/UI/UX constraints
- Security-agent decides security findings and requirements based on architecture review
- Developer-agent decides implementation details within approved contracts
- QA-agent decides validation results based on independent testing
- Documentation-agent decides documentation updates based on approved changes

The Orchestrator coordinates but does not dictate the specialist's professional judgments within their domain.

## Human Gates

Four mandatory Human gates must be explicitly approved:
1. Product Approval (after product-agent)
2. Architecture + Security Approval (after ui-ux, architect, and security pre-review)
3. Implementation Review (after developer-agent implementation and validation)
4. Final Human Validation (after Full QA, final security audit, and documentation)

Each gate requires an explicit Human message in the Orchestrator conversation. Automatic task completion does not imply approval.

## QA/Security Separation

- QA and Security are independent specialist agents
- QA validates against product acceptance criteria and regression behavior
- Security reviews architecture pre-implementation and audits final implementation against approved security requirements
- Neither QA nor Security implements product code
- Findings from either agent route corrections through the Orchestrator to the responsible specialist

## Correction Loops

When a Human gate rejects a phase or a specialist finds an issue:
- The Orchestrator routes the smallest responsible correction to the appropriate specialist
- Previously approved phases are preserved whenever safe
- Correction loops may target: product-agent, ui-ux-agent, architect-agent, security-agent, developer-agent, qa-agent, or documentation-agent
- The Orchestrator does not restart entire workflows unnecessarily

## Evidence/Handoff Model

Each specialist must produce verifiable evidence:
- Product-agent: requirements and acceptance criteria document
- UI/UX-agent: design specification
- Architect-agent: implementation architecture/plan
- Security-agent: review findings and requirements
- Developer-agent: implementation summary, validation evidence, file changes
- QA-agent: independent validation results
- Documentation-agent: required documentation changes

The Orchestrator validates that required evidence exists before allowing progression to the next phase. Handoffs are inspected for correctness and completeness.

## What This Architecture Does Not Include

This governance architecture does not specify or assume:
- Specific technical infrastructure (CI/CD systems, testing frameworks, etc.)
- Particular programming languages or frameworks
- Specific tools beyond the Hermes agent system
- Automatic technical enforcement of governance rules
- Deployment infrastructure or environments
- Specific Git hosting providers or repository structures

The architecture focuses solely on the governance model: roles, responsibilities, workflow sequence, Human approval requirements, and evidence-based handoffs.