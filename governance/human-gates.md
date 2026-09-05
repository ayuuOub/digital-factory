# Human Approval Gates in the Digital Factory

This document describes the four mandatory Human gates in the governed workflow and the separate explicit authorizations required for Git operations and deployment.

## The Four Mandatory Human Gates

### 1. Product Approval
- **When**: After the product-agent completes the Product requirements (including acceptance criteria).
- **What**: The Human reviews the product-agent's output to ensure it correctly captures the desired product behavior, scope, and acceptance criteria.
- **Outcome**: 
  - If approved, the workflow proceeds to UI/UX.
  - If rejected, the Human provides reasons and the Orchestrator routes a minimal product-agent correction.

### 2. Architecture + Security Approval
- **When**: After the ui-ux-agent, architect-agent, and security-agent (Security Pre-Review) have completed their tasks.
- **What**: The Human reviews the outputs of UI/UX, Architecture, and Security Pre-Review for consistency with the approved Product requirements and with each other.
- **Outcome**:
  - If approved, the workflow proceeds to Developer implementation.
  - If rejected, the Human provides reasons and the Orchestrator routes corrections to the responsible specialist(s).

### 3. Implementation Review
- **When**: After the developer-agent completes implementation and performs Developer-level validation.
- **What**: The Human reviews the developer-agent's output, including:
  - Implementation summary
  - Files created, modified, deleted
  - Validation commands and results
  - Evidence of Product contract preservation
  - Evidence of Security contract preservation
  - Limitations or failures noted by the Developer
  - Git status (commit not yet performed)
- **Outcome**:
  - If approved, the Human explicitly authorizes the Developer to create the approved commit.
  - If rejected, the Human provides reasons and the Orchestrator routes a minimal developer-agent correction.
  - Note: Approval of implementation does NOT authorize commit, push, or deployment.

### 4. Final Human Validation
- **When**: After:
  - QA-browser-validation-agent completes Full QA (PASS)
  - security-agent completes Final Implementation Security Audit (PASS)
  - documentation-agent completes required documentation updates (if any)
- **What**: The Human reviews the overall change to ensure it meets the original request and all governance requirements.
- **Outcome**:
  - If approved, the change is declared COMPLETE.
  - If rejected, the Human provides reasons and the Orchestrator routes corrections to the responsible specialist(s).
  - Note: Final Human Validation does NOT automatically authorize push or deployment.

## Separate Explicit Authorizations

The following Git and deployment operations require separate explicit Human authorization, even after the relevant Human gates have been passed:

### Commit Authorization
- **When**: After Human Implementation Review approves the implementation.
- **What**: The Human explicitly authorizes the Developer to create the approved commit.
- **Note**: This is a distinct step from Implementation Review approval.

### Merge Authorization
- **When**: After an authorized commit exists and is ready to be integrated into the target branch.
- **What**: The Human explicitly authorizes the merge operation.
- **Note**: Merge authorization is separate from commit authorization.

### Push Authorization
- **When**: After an authorized commit (and merge, if applicable) exists and is ready to be shared with remote repositories.
- **What**: The Human explicitly authorizes the push operation.
- **Note**: Push authorization is separate from merge and commit authorization.

### Deployment Authorization
- **When**: After an authorized push (if applicable) exists and is ready to be deployed to a target environment.
- **What**: The Human explicitly authorizes the deployment operation.
- **Note**: Deployment authorization is separate from push authorization and is not a Git command.

### Destructive/Guarded Git Operations
Operations that discard history or state (e.g., reset, clean, restore, rebase, amend, force push) require explicit Human authorization each time they are requested, regardless of other approvals.

## Key Distinctions

- **Implementation approval** (Gate 3) only confirms that the implementation is correct according to the approved contracts.
- **Commit authorization** is a separate explicit Human act that permits the Developer to record the approved implementation as a Git commit.
- **Merge authorization** is a separate explicit Human act that permits integrating the commit into a target branch.
- **Push authorization** is a separate explicit Human act that permits sharing the commit(s) with remote repositories.
- **Deployment authorization** is a separate explicit Human act that permits releasing the code to a target environment.

Final Human Validation (Gate 4) does NOT automatically authorize any of these operations. Each must be explicitly granted by the Human at the appropriate time.