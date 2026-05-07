---
name: creating-skills
description: "Use when the user asks to create a new Antigravity skill from scratch, convert documentation into a skill, or scaffold a skill directory structure - covers SKILL.md authoring, frontmatter standards, and skill validation"
---

# Creating Skills

## Overview

Generate high-quality, predictable `.agent/skills/` directories from user requirements. This skill covers the structural, stylistic, and validation rules for authoring Antigravity skills.

**REQUIRED BACKGROUND:** You MUST understand `.agent/skills/writing-skills/SKILL.md` before using this skill. That skill defines the TDD-based skill creation philosophy. This skill provides the concrete structural template and authoring rules.

## When to Use

- User asks to create a new skill
- User wants to convert an existing document or process into a skill
- User wants to scaffold a skill directory
- User asks how to structure a `SKILL.md`

## When NOT to Use

- Editing or refactoring an existing skill → use `writing-skills`
- Testing a skill under pressure scenarios → use `writing-skills` (TDD sections)
- One-off project conventions → put in `.agent/AGENTS.md` instead

## Directory Structure

Every skill follows this hierarchy:

```
<skill-name>/
  SKILL.md              # Required: Main logic and instructions
  scripts/              # Optional: Helper scripts and utilities
  examples/             # Optional: Reference implementations
  resources/            # Optional: Templates or assets
```

Keep it flat. Only add subdirectories when content exceeds what fits inline.

## YAML Frontmatter Standards

The `SKILL.md` MUST start with YAML frontmatter:

```yaml
---
name: gerund-skill-name
description: "Use when [specific triggering conditions]. Third person, max 1024 chars."
---
```

**Rules:**

- **name**: Gerund form preferred (e.g., `testing-code`, `managing-databases`). Max 64 chars. Lowercase, numbers, hyphens only. No "claude" or "anthropic".
- **description**: Written in third person. Start with "Use when..." to focus on triggers, NOT workflow summary. Max 1024 chars total.

### Description Anti-Patterns

```yaml
# ❌ BAD: Summarizes workflow
description: "Creates skills by first scaffolding, then validating frontmatter, then testing"

# ❌ BAD: First person
description: "I help create skills when the user needs them"

# ❌ BAD: Too vague
description: "For skill creation"

# ✅ GOOD: Triggering conditions only
description: "Use when the user asks to create a new Antigravity skill, convert a document into a skill, or scaffold a skill directory"
```

## Writing Principles

- **Assume intelligence**: Don't explain basics. Focus on the unique logic of the skill.
- **Progressive disclosure**: Keep `SKILL.md` under 500 lines. Link to secondary files (one level deep) for heavy reference.
- **Forward slashes**: Always use `/` for paths.
- **Degrees of freedom**:
  - **Bullet points** → high-freedom tasks (heuristics, judgment calls)
  - **Code blocks** → medium-freedom (templates, patterns)
  - **Specific commands** → low-freedom (fragile or exact operations)

## SKILL.md Template

```markdown
---
name: skill-name-here
description: "Use when [triggering conditions and symptoms]"
---

# Skill Title

## Overview

Core principle in 1-2 sentences.

## When to Use

- [Trigger / symptom 1]
- [Trigger / symptom 2]
- When NOT to use: [counter-cases]

## Checklist

- [ ] Step 1
- [ ] Step 2
- [ ] Step 3

## Workflow

[Flowchart ONLY if decision logic is non-obvious, otherwise numbered list]

## Instructions

[Specific logic, code snippets, or rules]

## Common Mistakes

[What goes wrong + fixes]

## Resources

- [Link to scripts/ or resources/ if applicable]
```

## Workflow & Feedback Loops

For complex skills, include:

1. **Checklists** — markdown checklists the agent writes to the `<appDataDir>/brain/<conversation-id>/task.md` artifact to track state
2. **Validation loops** — Plan-Validate-Execute pattern (e.g., run `--help` before applying changes)
3. **Error handling** — scripts should be "black boxes"; tell the agent to run `--help` if unsure

## Token Efficiency

Skills may load into every conversation. Keep them lean:

| Skill Type | Target |
|------------|--------|
| Getting-started workflows | < 150 words |
| Frequently-loaded skills | < 200 words |
| Standard skills | < 500 words |

**Techniques:**

- Reference `--help` instead of documenting all flags
- Cross-reference other skills instead of repeating content
- One excellent example beats five mediocre ones
- Compress examples ruthlessly

## Validation Checklist

After creating any skill, verify:

- [ ] `SKILL.md` exists in `<skill-name>/` directory
- [ ] YAML frontmatter has `name` and `description` (only these two fields)
- [ ] `name` uses lowercase letters, numbers, hyphens only
- [ ] `description` starts with "Use when..." and is third person
- [ ] `description` does NOT summarize the skill's workflow
- [ ] No legacy tool references (`Skill tool`, `Task tool`, `TodoWrite`, etc.)
- [ ] Forward slashes for all paths
- [ ] Under 500 lines total
- [ ] Cross-references use explicit requirement markers (`**REQUIRED SKILL:**`)
- [ ] No `@` links (they force-load files and burn context)

## Quick Reference

| Element | Rule |
|---------|------|
| Naming | Gerund, verb-first (`creating-X` not `X-creation`) |
| Frontmatter fields | Only `name` and `description` |
| Description style | "Use when..." + third person + triggers only |
| Max description | 1024 chars |
| Max SKILL.md | 500 lines |
| Path separators | Forward slashes only |
| Flowcharts | Only for non-obvious decisions |
| Examples | One great one, not multi-language |
| Cross-refs | `**REQUIRED SKILL:**` markers, no `@` links |
