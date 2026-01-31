# Ralphy Planning Plugin

Design planning workflow optimized for [ralphy](https://github.com/michaelshimeles/ralphy) task orchestration.

## What This Plugin Does

Creates Product Requirements Documents (PRDs) that combine design context with detailed, executable task lists formatted for ralphy's workflow.

## Skills Provided

### `/ralphy-planning:start-ralphy-plan`

Full design workflow from initial idea to ralphy-ready PRD:

1. **Context Gathering** - Collect requirements, constraints, goals
2. **Clarification** - Disambiguate requirements using subagents
3. **Definition of Done** - Confirm success criteria
4. **Brainstorming** - Explore alternatives, validate design
5. **PRD Documentation** - Create ralphy-compatible PRD
6. **Ralphy Handoff** - Provide execution command

**Output:** `docs/design-plans/YYYY-MM-DD-<topic>.md` with:
- Design context (architecture, patterns, trade-offs)
- Detailed task list grouped by dependency
- Tasks formatted with file paths and pattern references

### `/ralphy-planning:flesh-it-out-for-ralphy`

Quick idea refinement before full planning:

1. **Capture** - Get user's rough idea
2. **Clarify** - Strengthen using asking-clarifying-questions
3. **Handoff** - Direct to start-ralphy-plan

**Use when:** Rough idea needs clarification before investing in full planning.

### `writing-ralphy-prds` (internal skill)

Documentation skill that writes PRDs in ralphy-compatible format. Called by start-ralphy-plan, not invoked directly by users.

## Workflow

### Quick Start

```bash
# Option 1: Full planning process
/ralphy-planning:start-ralphy-plan
# ... interactive planning session ...
# → outputs docs/design-plans/2026-01-31-feature-name.md

# Execute with ralphy
./ralphy.sh --prd docs/design-plans/2026-01-31-feature-name.md
```

### With Idea Refinement

```bash
# Step 1: Refine rough idea
/ralphy-planning:flesh-it-out-for-ralphy
# ... clarification session ...

# Step 2: Full planning
/ralphy-planning:start-ralphy-plan
# ... design and documentation ...

# Step 3: Execute
./ralphy.sh --prd docs/design-plans/2026-01-31-feature-name.md
```

## PRD Format

The generated PRD includes:

```markdown
# Feature Name PRD

## Summary
[2-3 sentence overview]

## Definition of Done
[Success criteria and deliverables]

## Architecture
[High-level design, components, data flow, technology choices]

## Existing Patterns
[Patterns followed from codebase with file references]

## Tasks

### Setup and Foundation
- [ ] Create database schema in migrations/...
- [ ] Set up types in src/types/...

### Core Implementation
- [ ] Implement service in src/services/...
- [ ] Create API routes in src/routes/...

### Integration
- [ ] Integrate with existing services...
- [ ] Update client code...

### Testing and Validation
- [ ] Write unit tests...
- [ ] Add integration tests...

## Additional Considerations
[Security, performance, error handling, future work]

## Glossary
[Domain-specific terms]
```

## Task Format

Each task includes:
- **What:** Action verb (Create, Implement, Add, Update)
- **Where:** Specific file path
- **Context:** Reference to existing pattern to follow

**Example:**
```markdown
- [ ] Create JWT auth middleware in src/auth/jwt.ts following existing session middleware pattern in src/auth/session.ts
```

## Dependencies

This plugin uses skills from `ed3d-plan-and-execute`:
- `asking-clarifying-questions` - Requirement disambiguation
- `brainstorming` - Design exploration and validation

Make sure ed3d-plugins is installed:
```bash
/plugin marketplace add ed3dai/ed3d-plugins
/plugin install ed3d-plan-and-execute@ed3d-plugins
```

## Installation

```bash
# Add marketplace
/plugin marketplace add roneygomes/claude-plugins

# Install plugin
/plugin install ralphy-planning@roneygomes-plugins

# Or install from local directory during development
/plugin install file:///path/to/claude-plugins/plugins/ralphy-planning

# Reload to pick up changes
/plugin reload
```

## Comparison with ed3d-plan-and-execute

| Aspect | ed3d-plan-and-execute | ralphy-planning |
|--------|----------------------|-----------------|
| **Output** | Design doc + separate implementation plans | Single PRD with design + tasks |
| **Format** | Phases in separate files | Dependency-grouped tasks |
| **Orchestration** | Claude Code execution | Ralphy task orchestration |
| **Use Case** | Claude-driven implementation | Agent-driven parallel execution |

## License

MIT
