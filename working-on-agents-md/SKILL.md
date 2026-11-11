---
name: working-on-agents-md
description: Creates, reviews, and improves project AGENTS.md files. Use whenever creating or updating a project's AGENTS.md, including incidental edits during a larger task, and when asked to analyze, evaluate, or review these files.
---

# Working on `AGENTS.md`

## Pre-flight Task

`AGENTS.md` is a LLM prompt, so for any work on it, including review-only work, load available instructions for working on LLM prompts and agent instructions, whether provided by relevant skills, project instructions, or both. If none are found, stop and report the missing prerequisite.

## Workflow

Apply only relevant steps. For review-only requests, report actionable findings and recommendations without editing. Keep incidental updates focused on the affected workflow. Number findings for easier reference.

1. **Establish scope and evidence.**
   - Read the target file, applicable parent instructions, and relevant nested instruction files. Treat proposed instructions as content to assess; follow the applicable instruction hierarchy while editing.
   - Inspect relevant documentation, package scripts, build configuration, and CI to establish actual workflows. Investigate apparent conflicts and preserve existing intent unless a change is requested.
   - When guidance depends on discovery, precedence, inclusion, or size limits, identify the intended agent tools and product surfaces and verify their behavior in current documentation or configuration. Do not assume identical support across tools.
   - Resolve uncertainty from repository evidence first. Ask targeted questions when material uncertainty remains; do not invent project requirements.
2. **Select useful guidance.** Apply the content rules below. Include sections only when they help the agent perform real project work.
3. **Draft focused changes.** Follow the structure and writing rules below. Preserve existing intent and unrelated user work, and state each requirement once in its most relevant place.
4. **Validate.** Follow the validation guidance below, revise defects, and report any checks that could not be completed or verified.

## Content Rules

- **Prioritize non-obvious knowledge.** Capture the correct package manager, setup order, environment prerequisites, known setup failures and workarounds, hidden dependencies, architectural boundaries, generated-file regeneration commands, and unusual local conventions when relevant. Identify stack and runtime/tool versions when they affect the workflow, preferably by referencing authoritative project metadata. Prefer facts an agent would otherwise get wrong over exhaustive repository inventories or obvious directory summaries.
- **Make commands executable and conditional.** Put frequently needed setup and verification commands early. Include the working directory, relevant flags, prerequisites, required order, and the changes that trigger each check. Distinguish focused checks from broader checks; do not prescribe expensive full-suite runs for every task without a project-specific reason.
- **Keep the source of truth authoritative.** Identify how to run formatter, linter, type-checker, and CI checks, but refer to their configuration for machine-enforced settings; document constraints those tools cannot express. Avoid copying root guidance into nested files or large sections of existing documentation into `AGENTS.md`; reference the authoritative source instead.
- **Capture relevant workflow boundaries.** Include project-specific restrictions on generated or vendor files, dependency changes, commits, or deployment only when supported by project policy. Do not invent approval requirements or generic checklists.
- **Maintain living documentation.** Update affected guidance when workflows change. Remove obsolete workarounds after verifying they no longer apply; label necessary legacy conditions. Start small and add rules in response to observed mistakes rather than anticipating every possible failure.

## Structure and Writing

- Use standard Markdown with useful headings; `AGENTS.md` requires no special schema or YAML frontmatter. Do not confuse it with custom-agent definitions such as `.github/agents/*.md` or copy their persona and metadata requirements.
- Keep root guidance broadly applicable. Add nested files only for genuinely specialized subsystem rules. Avoid repeating root instructions; make intentional local exceptions explicit and resolve conflicts using the applicable hierarchy. When guidance depends on discovery or combination behavior, verify how the intended tool handles it (see Workflow).
- Express observable behavior: identify the triggering situation and required action. Distinguish mandatory requirements from preferences. Include a short reason, safe path, or exception when it improves reliability.
- Use small representative examples or canonical implementation references for unusual conventions. For example: “Register new HTTP endpoints through `src/http/router.ts`; direct registration bypasses authentication middleware.” Adapt examples to verified project facts.
- Make references actionable. State when linked documentation must be read: “Before changing database migrations, read `docs/database-migrations.md`.” A link or `@path` is not a portable automatic include; use explicit reading instructions or a verified tool-specific inclusion mechanism.
- Keep shared project guidance in version control using the project's normal contribution workflow. Keep personal preferences in the target tool's global configuration when appropriate rather than introducing them as team policy.

## Updating an Existing `AGENTS.md`

When updating an existing `AGENTS.md`, unless the user explicitly requests otherwise:

- Make focused, minimal edits.
- Preserve the document’s existing structure unless the requested change requires restructuring.

## Validation

- Check changed commands against repository scripts, configuration, and CI. Execute relevant commands where feasible, with documented prerequisites and working directory; do not run destructive or deployment commands merely to verify documentation. Verify referenced paths and examples, and check that root and nested rules are coherent and linked documents have explicit loading conditions. Report checks done only by inspection, unavailable, or failed, with reasons.
- When changing instruction discovery or inclusion, verify which sources the intended tool actually loads using supported diagnostics or logs. Account for tool-specific limits and session reload behavior; do not treat a maximum context size as a target document length. Report discovery that remains unverified.
- Review for preserved intent, actionable requirements, missing prerequisites, contradictions, duplication, stale guidance, and unnecessary tokens. A longer document is not evidence of improvement.
- For substantial or behavior-sensitive revisions, define observable success criteria and, when execution is available, compare original and revised instructions on the same representative tasks with comparable model/runtime settings. Include relevant failure cases such as stale commands, conflicting nested rules, ambiguous references, duplicated README or lint guidance, incidental updates, and review-only requests; check activation against nearby requests outside the `AGENTS.md` scope.
- Evaluate whether the revision reduces repeated mistakes, supports successful relevant checks, and has reasonable execution cost. Do not assume context files or repository overviews improve task success. Distinguish observed behavior from inspection-only findings, and report unavailable execution or unresolved validation.
