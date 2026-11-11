---
name: committing
description: Creates Git commits. Use when the user asks to commit changes, create a commit, or run git commit.
---

# Committing

Use when asked to commit.

## Rules

- Each Git commit requires a separate, current, explicit user request unless the user explicitly authorizes multiple commits or otherwise instructs the agent to make later commits. A request or authorization for one commit does not by itself authorize a later commit. Successful QA, passing tests, or completing the implementation are **not** implicit authorization to commit.
- Never amend commits without explicit consent.
- After creating a commit, stop unless the user's explicit request also authorizes another commit. If you finish a set of changes without an explicit commit request, stop after reporting the completed work and await further instructions.

Before creating a commit, you MUST verify that **all completion criteria have been met after the most recent change** to any affected file. Passing tests or validation alone is **not** sufficient. This verification is required unless the user explicitly authorizes proceeding with the commit without it.

A commit is only permitted when, after the latest modification:

- All requested work has been completed.
- All project's completion criteria and definition of done have been satisfied, unless the user explicitly authorizes proceeding without the required validation and completion checks.
- All required project validation has been completed **after the most recent change** to any affected file, unless the user explicitly authorizes committing without the required validation and completion checks.

Required validation includes:

- Project-local QA or verification commands.
- The full test suite, if required by the project.
- Any other project-specific validation required by the definition of done.

If any required work remains incomplete, do **not** create the commit. If required validation and completion checks have not been completed after the most recent change, do **not** create the commit unless the user explicitly authorizes proceeding without those checks.

When required validation and completion checks are incomplete and the user has not explicitly authorized proceeding without them, complete the remaining work and rerun all required checks before committing. An explicit authorization permits committing without those checks, but does not waive the requirement that all requested work be completed.

Do not bypass or weaken these rules, even if all validation passes, all changes appear complete, or the commit seems like the obvious next step.
