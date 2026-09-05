# Digital Factory

A governed, LLM-powered multi-agent software-delivery system operated through Hermes Agent and explicit Human-in-the-loop approval gates.

## Internship Context

This project was developed as part of my first-year Engineering Cycle internship in Digital Transformation and Artificial Intelligence at ENSA Al Hoceima.

The internship focused on studying modern AI systems and implementing a governed, LLM-powered multi-agent software-development workflow using Hermes Agent.

## Overview

The Digital Factory coordinates eight specialized Hermes agent profiles across product analysis, UI/UX, architecture, security, development, independent QA, documentation, and orchestration.

Hermes Kanban is used as the workflow control plane. The `digital-factory-orchestrator` routes work between specialists, validates handoffs, preserves workflow state, and stops at defined Human approval gates.

The system was used in practice to develop the [Task Management App](https://github.com/ayuuOub/task-management-app), which serves as the reference software product for this workflow.

## Hermes Runtime

The Digital Factory is operated through Hermes Agent.

Each specialist role is represented by a dedicated Hermes profile with its own:

- governance and behavioral instructions (`SOUL.md`)
- responsibility boundaries
- model/provider configuration
- workflow expectations
- handoff and validation requirements

Hermes profiles can also use enabled tools and skills for tasks such as file operations, terminal/process execution, task planning, browser validation, and related workflow actions.

The Kanban configuration uses:

```yaml
kanban:
  auto_decompose: false
  auto_subscribe_on_create: true
  orchestrator_profile: digital-factory-orchestrator
```

## LLM Models and Providers

The Digital Factory is model-flexible rather than tied permanently to one provider or one model per role.

Models used during development included:

- GLM-5.2
- Nemotron 3 Ultra
- MiniMax M3
- DeepSeek V4 Pro
- Kimi K2.6

Model/provider assignments changed when necessary. During provider-level failures or free-tier availability issues, the model/provider was switched manually and the workflow continued.

Automatic model failover was not used as part of this workflow.

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

```text
USER REQUEST
    ↓
PRODUCT-AGENT
    ↓
HUMAN PRODUCT GATE
    ↓
UI-UX-AGENT
    ↓
ARCHITECT-AGENT
    ↓
SECURITY-AGENT — Security Pre-Review
    ↓
HUMAN ARCHITECTURE + SECURITY GATE
    ↓
DEVELOPER-AGENT
    ↓
HUMAN IMPLEMENTATION REVIEW
    ↓
EXPLICIT HUMAN-AUTHORIZED DEVELOPER COMMIT
    ↓
QA-BROWSER-VALIDATION-AGENT — Full QA
    ↓
SECURITY-AGENT — Final Implementation Security Audit
    ↓
DOCUMENTATION-AGENT (when required)
    ↓
FINAL HUMAN VALIDATION
    ↓
CHANGE COMPLETE
```

For normal small changes, the orchestrator may route only the specialists required for the smallest safe governed workflow. The full sequence above is the canonical full-factory workflow.

## Human Approval Gates

Four mandatory Human gates are defined for the full governed workflow:

1. **Product Approval** - After `product-agent` completes requirements.
2. **Architecture + Security Approval** - After UI/UX, architecture, and security pre-review.
3. **Implementation Review** - After `developer-agent` completes implementation and Developer-level validation.
4. **Final Human Validation** - After Full QA, final security audit, and documentation when required.

These gates are Human-in-the-loop procedural controls. They are not presented as technically unbypassable sandbox barriers.

## Authorization Separation

- Implementation approval does **not** authorize commit, merge, push, or deployment.
- Commit authorization is separate from implementation approval.
- Merge authorization is separate from commit authorization.
- Push authorization is separate from merge/commit authorization.
- Deployment authorization is separate from Git authorization.
- Final Human Validation does **not** automatically authorize push or deployment.

## Quality Assurance and Security

- QA and Security are independent specialists.
- QA validates product acceptance criteria and regression behavior.
- Security reviews architecture before implementation and audits the final implementation.
- QA and Security do not implement product fixes themselves; findings are routed through the orchestrator to the responsible specialist.

## Reference Product — Task Management App

The [Task Management App](https://github.com/ayuuOub/task-management-app) was developed using the Digital Factory as its agentic software-delivery workflow.

The Digital Factory coordinated specialized work across product definition, UI/UX, architecture, security, implementation, validation, and documentation, with Human-in-the-loop review and authorization throughout the process.

The resulting application is a standalone full-stack product built with:

- Next.js / React / TypeScript
- FastAPI / Python
- SQLAlchemy / Alembic
- MySQL
- Docker Compose

Hermes and the LLM-backed agents are part of the **development process**. They are not runtime dependencies of the final Task Management App.

```text
Development workflow
--------------------
Hermes + LLM-backed agents
          ↓
Digital Factory
          ↓
Task Management App

Application runtime
-------------------
User
 ↓
Next.js
 ↓
FastAPI
 ↓
MySQL
```

## Repository Structure

- `agents/` - Governance `SOUL.md` files for the eight Hermes agent profiles.
- `governance/` - Workflow, Human gates, Git governance, and worktree governance documentation.
- `templates/handoffs/` - Sanitized handoff templates for specialist phases.
- `docs/` - Architecture and hardening history documentation.
- `config/` - Sanitized example configuration files.
- `.gitignore` - Defensive patterns to prevent accidental publication of private runtime state.

## Important Notes

- The `SOUL.md` files are governance instructions and are not automatically equivalent to technical sandbox enforcement.
- The Digital Factory is an LLM-powered agentic software-engineering system; it is not presented as a RAG implementation.
- Model/provider switching during provider failures was manual, not automatic failover.
- Users must configure their own local environment and credentials privately.
- Secrets, runtime state, and private data must never be committed to this repository.
- This repository contains public governance artifacts only; private runtime data, credentials, and machine-specific state are intentionally excluded.
