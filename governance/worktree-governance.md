# Worktree Governance in the Digital Factory

This document describes the governance rules for assigned worktrees in the Digital Factory workflow.

## Assigned-Worktree Boundaries

Each specialist agent (and the Orchestrator when performing read-only inspection) operates within an assigned worktree that is isolated to their task.

- The worktree is provided by the Orchestrator via the Kanban task workspace.
- The agent must not modify files outside of their assigned worktree unless explicitly authorized by a Human for a specific, shared purpose (which is rare and must be justified).
- The agent must preserve unrelated changes that may exist in the worktree (e.g., if the worktree is shared across multiple tasks in a project-linked scenario, though by default each task gets a fresh worktree).

## Preserve Unrelated Changes

If a worktree contains changes that are not part of the current task (for example, in a linked project scenario where the worktree is shared), the agent must:

- Not overwrite or discard those unrelated changes.
- Ensure their work does not conflict with or break those unrelated changes.
- If a conflict arises, the agent must report it as a blocker and await Human resolution.

## Report Unexpected Dirty State

At the start of a task, if the agent finds the worktree in an unexpected dirty state (i.e., there are uncommitted changes that are not part of the task's assigned work), the agent must:

- Stop work.
- Report the unexpected state as a blocker to the Orchestrator (via Kanban comment or by blocking the task).
- Not proceed until the Human has resolved the state (e.g., by stashing, committing, or discarding the changes with explicit authorization).

## No Automatic Reset/Clean/Restore/Delete

The agent must not perform any of the following operations on the worktree without explicit Human authorization:

- `git reset` (especially `--hard`)
- `git clean`
- `git restore` (to discard changes)
- Deleting the worktree

These operations are considered destructive and require explicit Human approval.

## No Modification of Another Specialist's Worktree

Each specialist's worktree is isolated. An agent must not:

- Modify another specialist's assigned worktree.
- Access another specialist's worktree to read or write files, even for inspection, unless the Orchestrator has explicitly provided the necessary artifacts via the handoff mechanism (e.g., through Kanban attachments or by copying approved specifications into the current agent's workspace).

Inspection of another specialist's work is done through the validated handoff artifacts, not by direct access to their worktree.

## Inspect Diffs Before Handoff

Before marking a task as complete and handing off to the next phase, the agent must:

- Inspect the diff of their changes in the worktree (using `git diff` or equivalent).
- Ensure the diff matches the expected scope of work as defined by the approved inputs and the agent's responsibility boundary.
- Ensure no extraneous files have been created or modified inadvertently.

## Destructive Cleanup Requires Exact Human Authorization

If the Orchestrator or a specialist requests a destructive cleanup of the worktree (e.g., to remove all uncommitted changes and untracked files), this requires:

- An explicit Human authorization message specifying exactly what is to be done (e.g., "Please run `git reset --hard && git clean -fd` on the worktree for task XYZ").
- The Human must understand and approve the specific destructive action.

## Worktree Safety Summary

- Assigned worktrees are sacred spaces for the specialist to perform their work.
- The Orchestrator is responsible for providing clean, isolated worktrees by default.
- Specialists must preserve the integrity of the worktree and report any unexpected state.
- Destructive operations on the worktree are strictly controlled by Human authorization.