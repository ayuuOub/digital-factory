# Git Governance in the Digital Factory

This document describes the Git operations that are permitted with explicit Human authorization and those that are prohibited without such authorization in the Digital Factory workflow.

## READ-ONLY Git Inspection (No Authorization Required)

The following Git operations are considered read-only and do not require explicit Human authorization. They may be performed by any specialist agent or the Orchestrator for inspection purposes:

- `git status` - To inspect the current state of the worktree.
- `git diff` - To view changes between commits, commit and working tree, etc.
- `git log` - To view the commit history.
- `git show` - To view various types of objects (commits, tags, etc.).

These operations are safe because they do not modify the repository state.

## Explicit Human Authorization Requirements

The following Git operations require explicit Human authorization before they can be performed. Authorization must be granted for each specific operation and scope.

### 1. `git add` as part of an approved commit scope
- **When**: After Human Implementation Review has approved the implementation and before committing.
- **What**: The Human must explicitly authorize the specific files or changes to be added to the index as part of the approved commit scope.
- **Note**: The Human must review the exact set of changes to be staged. Blanket authorization to add all changes is not permitted without review.

### 2. `git commit`
- **When**: After the authorized `git add` has been staged.
- **What**: The Human must explicitly authorize the commit operation with the exact commit message and scope that was reviewed.
- **Note**: The Human must see the exact diff that will be committed. Authorization for a commit does not authorize any subsequent operations.

### 3. `git merge`
- **When**: After an authorized commit exists on a feature/topic branch and is ready to be integrated into the target branch (e.g., main).
- **What**: The Human must explicitly authorize the merge operation, including the specific source and target branches and the merge strategy (if non-default).
- **Note**: The Human must review the changes to be merged. Authorization for a merge does not authorize push or deployment.

### 4. `git push`
- **When**: After an authorized commit (and merge, if applicable) exists locally and is ready to be shared with remote repositories.
- **What**: The Human must explicitly authorize the push operation, including the specific remote, branch, and any required flags (e.g., `--tags`).
- **Note**: The Human must review the commits to be pushed. Authorization for a push does not authorize deployment.

## Guarded/Destructive Operations

The following Git operations are considered destructive or guarded because they can discard commits, history, or working tree changes. Each requires explicit Human authorization every time they are requested, and the Human must be presented with a clear explanation of what will be lost.

- `git reset` (especially `--hard` or when moving HEAD)
- `git clean` (removing untracked files)
- `git restore` (restoring files to a previous state, potentially overwriting changes)
- `git rebase` (rewriting commit history)
- `git commit --amend` (modifying the most recent commit)
- State-discarding `git checkout` or `git switch` (when discarding changes in the working tree)
- Force push (`git push --force` or `--force-with-lease`)
- Any operation that rewrites history (e.g., `git filter-branch`, `git filter-repo`)

## Key Principles

### No Automatic Git Operations
- No automatic commit.
- No automatic merge.
- No automatic push.
- No automatic deployment.

Each of these operations must be explicitly authorized by a Human at the appropriate time in the workflow.

### Authorization is Specific and Scoped
Human authorization for Git operations must be specific to the operation, the scope (files, branches, commits), and the intended outcome. Blanket authorizations are not permitted.

### Separation of Concerns
- Implementation approval (Gate 3) does not authorize commit.
- Commit authorization does not authorize merge.
- Merge authorization does not authorize push.
- Push authorization does not authorize deployment.

Each step requires a separate explicit Human authorization.

### Do Not Describe Deployment as a Git Command
Deployment is a separate operational step that may involve copying artifacts, restarting services, or other non-Git actions. It is not a Git command and requires its own explicit Human authorization.

## Workflow Integration

In the Digital Factory workflow:
1. After Human Implementation Review approves the implementation, the Human must explicitly authorize the Developer to perform `git add` (specific files) and `git commit`.
2. After the commit is created, if a merge is required, the Human must explicitly authorize the `git merge`.
3. After the merge (if any) is complete, the Human must explicitly authorize the `git push`.
4. Deployment, if required, requires a separate explicit Human authorization after the push.

At no point are these operations automatic or bundled together.