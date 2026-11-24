---
name: working-on-agent-skills
description: Creates, reviews, and improves Agent Skills, including SKILL.md metadata, instructions, and supporting resources. Use when asked to create, analyze, evaluate, edit, or improve an Agent Skill or SKILL.md file.
---

# Working on Agent Skills

Skills help users perform repetitive tasks through reusable instructions. This skill guides their creation, review, and improvement so those tasks can be performed consistently.

## Core Principles

- Prefer direct instructions and concrete examples over abstract discussion.
- Use consistent terms and durable guidance. Remove temporary details or label necessary legacy information; omit redundant guidance and nearby conventions unless needed for this skill to work reliably.

---

## Required Coverage

Every skill must clearly cover these four areas, using sections appropriate to its purpose:

- **Work:** Define the workflow, when it applies, its scope, required inputs, and expected outputs.
- **Rationale:** Explain why the work is needed and the rationale for non-obvious requirements. Keep explanations brief, grounded, and useful for making decisions. Ask the user if not clear.
- **Rules and guidelines:** State mandatory constraints and prohibitions explicitly. Distinguish them from recommendations, defaults, and permitted exceptions.
- **Completion criteria:** Define observable conditions for considering the work complete, including how to check outputs and how to report unmet or unverified requirements.

---

## Pre-flight Task

1. **Apply prompt-writing guidance.** Before reviewing or editing `SKILL.md` or reference documents, load and read LLM prompt and agent instructions guidance as those files are agent instructions, therefore you must apply LLM prompt instructions to them.
2. **Establish the task requirements.** Use the request and available context to identify:
   - **Inputs:** The requested operation, target capability, and applicable requirements. For reviews or revisions, include the existing skill and relevant supporting resources.
   - **Expected outputs:** The deliverables and their scope, such as a new or revised skill package, review findings, or an explanation.

If required information is missing or materially unclear, ask the user before proceeding. Do not invent requirements or ask the user to repeat information already supplied.

---

## Workflow

Apply only the steps relevant to the request.

1. **Analyze the request and skill.** Identify objective, scope, constraints, inputs, outputs, triggers, ambiguities, and known failure cases. For existing skills, establish the current behavior.
2. **Define the capability.** Focus on one clear, reusable capability. Prefer specific, activity-focused names, often in gerund form.
3. **Draft or revise metadata and instructions.** Ensure the instructions address all four required coverage areas. Match specificity to risk.
4. **Add supporting material when useful.** Include workflows, examples, templates, references, or scripts only when they improve clarity or reliability.
5. **Review and validate.** Review against the completion criteria below. For creation or revision, fix failed checks within the requested scope and repeat them. Report checks that are out of scope, blocked, or unverified. For reviews or explanations, report findings without editing.

---

## Metadata

Use the [Agent Skills specification](https://agentskills.io/specification) as the format baseline. Every `SKILL.md` must contain YAML frontmatter with `name` and `description`, followed by Markdown instructions. Create or update frontmatter as needed. In the Name and Description subsections, explicitly stated format and length limits are mandatory; other guidance in those two subsections is advisory.

### Name

- The name must be 1–64 characters, use only lowercase letters, numbers, and hyphens, and match the containing directory name. It must not start or end with a hyphen or contain consecutive hyphens.
- Prefer a specific, descriptive, activity-focused name. Gerund forms such as `processing-pdfs` are a useful convention.
- Avoid vague or overly broad names.

### Description

- State what the skill does and when to use it. Agents use descriptions to select relevant skills before loading their full instructions.
- Include domain terms and trigger phrases that distinguish it from other skills.
- The description must be nonempty and at most 1,024 characters.
- Prefer capability-first, third-person wording.
- Avoid generic descriptions and backticks.

---

## Instructions And Workflows

- Use only sections that serve the skill's purpose; do not add sections solely to match a template.
- Keep the main `SKILL.md` focused and under 500 lines as a guideline, because its entire contents load when the skill is activated.
- For multi-step tasks, order the steps as they should be performed and identify required inputs and expected outputs.
- Use flexible guidance where multiple approaches are valid. State a preferred pattern with parameters when a useful default exists.
- Add validation before irreversible or high-impact actions, and explain recovery when validation fails.
- Define how to check outputs against requirements, a style guide, or a validator. The Agent Skills reference validator checks frontmatter and naming conventions, not whether instructions produce the intended behavior.

---

## References, Examples, Scripts, And Assets

- Use progressive disclosure when substantial reference material would distract from the main instructions. Supporting resources load only when needed, conserving context. Store supporting documentation in `references/`, executable utilities in `scripts/`, and templates or static resources in `assets/` when useful.
- Reference bundled files using paths relative to the skill root. Use Markdown links for documentation, such as `[Reference guide](references/file-name.md)`, and explicit paths or commands for scripts and assets. Link resources directly from `SKILL.md`; avoid reference chains.
- State when and how each resource should be used: read documentation, execute or inspect scripts, or copy, populate, or transform assets. Paths alone do not load or execute resources. For commands, explain how to resolve skill-relative paths when the working directory differs from the skill root.
- Split references by task or domain when that keeps unrelated details out of the main skill. Give files descriptive names, use forward slashes, add a table of contents to references over 100 lines, and remove unused or duplicate material.
- Include examples when they clarify expected behavior; use exact templates for strict output requirements and label adaptable templates as defaults.
- Avoid listing alternatives unless a choice is required; give a recommended default and relevant exception.
- Prefer maintained utility scripts for deterministic, repeatable operations when appropriate. State whether to execute a script or consult it as reference.
- Document dependencies, execution requirements, configuration, and non-obvious constants. Follow project dependency conventions; do not assume installation is available or permitted.
- Make script errors actionable. Fail clearly when recovery could conceal invalid input or produce misleading output; use defaults only when they are correct.
- Validate plans and intermediate data before batch, destructive, or high-impact operations. Use visual inspection when rendered output reveals relevant structure that text extraction cannot.

---

## Updating an Existing Skill Document

When updating an existing document, make focused, minimal edits within the requested scope. Preserve intent unless a behavior change is requested, and preserve existing structure unless the requested change requires restructuring.

---

## Completion Criteria

For creation or revision, apply these criteria to the resulting prompt. For reviews or explanations, use them to assess the prompt and report findings.

Review the instructions internally against these criteria. For substantial or behavior-sensitive changes, reason through representative tasks and known failure cases, including activation and non-activation cases when relevant. Do not run behavioral tests or compare prompt behavior using external tools or models. Internal review does not establish behavioral verification; do not report it as such.

- The name and description are specific and valid.
- Instructions are concise, actionable, consistent, and aligned with the skill's intended behavior.
- The skill clearly covers its work, rationale, rules and guidelines, and completion criteria.
- Examples match the instructions; references are directly linked and useful.
- Time-sensitive details are removed or clearly marked as legacy.
- Scripts, dependencies, and execution requirements follow project conventions; critical outputs and intermediate plans are validated.
- Internal review is complete, with identified issues addressed for creation or revision, or reported for reviews or explanations.
- Applicable project requirements for LLM prompts and agent instructions were followed.
