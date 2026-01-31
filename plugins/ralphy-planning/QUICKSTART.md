# Ralphy Planning - Quick Start Guide

## Installation

```bash
# Add marketplace
/plugin marketplace add roneygomes/claude-plugins

# Install plugin
/plugin install ralphy-planning@roneygomes-plugins
/plugin reload
```

## Verify Installation

After reloading, these skills should be available:
- `ralphy-planning:start-ralphy-plan`
- `ralphy-planning:flesh-it-out-for-ralphy`

## Usage Workflows

### Workflow 1: Full Planning (Recommended)

For clear ideas ready for detailed planning:

```bash
/ralphy-planning:start-ralphy-plan
```

This will:
1. Gather context from you
2. Clarify requirements using subagents
3. Confirm definition of done
4. Brainstorm design alternatives
5. Create ralphy-compatible PRD
6. Provide ralphy execution command

**Output:** `docs/design-plans/YYYY-MM-DD-<topic>.md`

**Execute with ralphy:**
```bash
./ralphy.sh --prd docs/design-plans/2026-01-31-my-feature.md
```

### Workflow 2: Idea Refinement → Planning

For rough ideas that need clarification first:

```bash
# Step 1: Clarify the rough idea
/ralphy-planning:flesh-it-out-for-ralphy
```

After clarification, the skill will direct you to:

```bash
# Step 2: Full planning
/ralphy-planning:start-ralphy-plan
```

Then execute with ralphy as above.

## What Gets Created

The PRD file includes:

1. **Design Context**
   - Summary
   - Definition of Done
   - Architecture (overview, components, data flow, tech choices)
   - Existing Patterns (with file references)
   - Additional Considerations (security, performance, etc.)
   - Glossary

2. **Ralphy Task List**
   - Tasks grouped by dependency (Setup → Core → Integration → Testing)
   - Each task includes: what to do, where (file path), pattern to follow
   - Format: `- [ ] Create X in path/to/file.ext following pattern from path/to/example.ext`

## Example PRD Task Section

```markdown
## Tasks

### Setup and Foundation
- [ ] Create database schema in migrations/2026_01_31_add_notifications.sql following migration pattern in migrations/2026_01_15_add_users.sql
- [ ] Set up TypeScript types in src/types/notification.ts matching interface style from src/types/user.ts

### Core Implementation
- [ ] Implement NotificationService class in src/services/NotificationService.ts following singleton pattern from src/services/UserService.ts
- [ ] Create API endpoints in src/routes/notifications.ts following REST conventions from src/routes/users.ts

### Integration
- [ ] Integrate NotificationService with existing WebSocket handler in src/websocket/index.ts
- [ ] Update client API calls in client/src/api/notifications.ts matching async/await pattern from client/src/api/users.ts

### Testing and Validation
- [ ] Write unit tests in tests/unit/NotificationService.test.ts following Jest pattern from tests/unit/UserService.test.ts
- [ ] Add E2E tests in tests/e2e/notifications.spec.ts following Playwright pattern from tests/e2e/users.spec.ts
```

## Running with Ralphy

Once your PRD is created:

```bash
./ralphy.sh --prd docs/design-plans/2026-01-31-my-feature.md
```

Ralphy will:
- Execute tasks in dependency order
- Assign tasks to isolated agents
- Track completion by marking tasks with `[x]`
- Handle merging and environment isolation

## Tips

1. **Let the brainstorming happen** - Don't skip the design exploration phase
2. **Answer clarifying questions** - Better upfront clarity = better tasks
3. **Review the PRD before executing** - Make sure tasks make sense
4. **Use existing patterns** - The PRD references existing code to follow
5. **Monitor ralphy progress** - Check the PRD file to see completed tasks

## Differences from ed3d-plan-and-execute

| Feature | ed3d | ralphy-planning |
|---------|------|----------------|
| Output | Separate design + implementation files | Single PRD file |
| Tasks | Split across phase files | Dependency-grouped in one file |
| Execution | Claude Code manual execution | Ralphy automated orchestration |
| Format | Implementation phases | Ralphy checkbox tasks |

## Dependencies

Requires `ed3d-plan-and-execute` for:
- `asking-clarifying-questions` skill
- `brainstorming` skill

Install if not already available:
```bash
/plugin marketplace add ed3dai/ed3d-plugins
/plugin install ed3d-plan-and-execute@ed3d-plugins
```

## Troubleshooting

**Skills not showing up:**
```bash
/plugin reload
/plugin list  # verify ralphy-planning is installed
```

**Missing dependencies:**
Install ed3d-plan-and-execute (see Dependencies above)

**PRD format not working with ralphy:**
Check that tasks use `- [ ]` checkbox format and file paths are specific

## Support

- Report issues: https://github.com/roneygomes/claude-plugins/issues
- Ralphy docs: https://github.com/michaelshimeles/ralphy
- Ed3d plugins: https://github.com/ed3dai/ed3d-plugins
