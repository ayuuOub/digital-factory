# Canonical Digital Factory Workflow

This document describes the standard sequence of operations for a governed change in the Digital Factory.

## Workflow Sequence

```
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

## Correction Loops

When a Human gate rejects a phase, the Digital Factory Orchestrator routes the smallest responsible correction to the appropriate specialist agent, preserving all previously approved phases whenever safe.

### Example Correction Flow

If Human Implementation Review finds a defect:
1. Human Review FAIL
2. Orchestrator creates targeted developer-agent correction task
3. Developer implements correction
4. Human retests the specific fix
5. If approved, continue to next phase (Full QA)

## Orchestrator Responsibilities

The Digital Factory Orchestrator:
- Understands the requested change
- Assigns or preserves a CHANGE_ID
- Determines current workflow phase
- Inspects relevant Kanban state
- Creates specialist Kanban tasks
- Assigns correct specialists
- Links dependencies correctly
- Preserves approved Product, UI/UX, Architecture, and Security contracts
- Enforces Human governance gates
- Routes targeted corrections when required
- Reports blockers accurately
- Maintains traceability from request to final validation

## Specialist Independence

Each specialist agent operates within their defined responsibility boundary:
- Product-agent: WHAT must be built (requirements, acceptance criteria)
- UI/UX-agent: interaction design, visual hierarchy, component states
- Architect-agent: implementation architecture, component boundaries, technical design
- Security-agent: security pre-review and final implementation audit
- Developer-agent: planned implementation and code changes within authorized workspace
- QA-agent: independent browser validation
- Documentation-agent: documentation updates when required
- Orchestrator: workflow coordination only — never implements product code

## Evidence-Based Handoffs

Each specialist must produce verifiable evidence of their work:
- Product: requirements and acceptance criteria
- UI/UX: actual design specification
- Architecture: implementation architecture/plan
- Security: actual review/findings
- Developer: actual implementation and validation evidence
- QA: actual independent validation results
- Documentation: required documentation changes

The Orchestrator validates handoffs before allowing progression to the next phase.

## Human Gate Authority

Human gates are the only authority that can approve progression between major workflow phases. Automatic task completion or Kanban state changes do NOT imply Human approval.

All Human approvals must be explicit messages in the Orchestrator conversation.