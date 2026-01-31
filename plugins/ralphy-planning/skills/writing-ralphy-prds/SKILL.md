---
name: writing-ralphy-prds
description: Use after brainstorming completes - writes validated designs to docs/design-plans/ in ralphy-compatible format with design context and detailed task lists
---

# Writing Ralphy-Compatible PRDs

## Overview

Transform validated design conversations into ralphy-compatible Product Requirements Documents (PRDs) that combine design context with detailed, executable task lists.

**Core principle:** Design context + grouped dependency-aware tasks = ralphy-ready PRD.

**Announce at start:** "I'm using the writing-ralphy-prds skill to create your ralphy-compatible PRD."

## Quick Reference

| Section | Purpose | Format |
|---------|---------|--------|
| **Summary** | 2-3 sentence overview | Markdown paragraph |
| **Definition of Done** | Success criteria | Bullet list |
| **Architecture** | High-level design | Subsections with details |
| **Existing Patterns** | Patterns followed | File references + descriptions |
| **Tasks** | Detailed task list for ralphy | `- [ ] task with context` |
| **Additional Considerations** | Edge cases, gotchas | Subsections as needed |

## File Location and Naming

**Path:** `docs/design-plans/YYYY-MM-DD-<topic>.md`

**Examples:**
- `docs/design-plans/2026-01-31-oauth2-service-auth.md`
- `docs/design-plans/2026-01-31-user-profile-api.md`
- `docs/design-plans/2026-01-31-websocket-notifications.md`

Use actual date and descriptive topic slug.

## Document Structure

```markdown
# [Feature Name] PRD

## Summary
[2-3 sentence overview of what's being built and why]

## Definition of Done
[Confirmed success criteria from planning]
- Primary deliverable
- Key acceptance criteria
- Explicit exclusions (if any)

## Architecture

### Overview
[High-level architecture description]

### Components
[Key components and their responsibilities]

### Data Flow
[How data moves through the system]

### Technology Choices
[Technologies selected and why]

## Existing Patterns

### [Pattern Name]
**Location:** `path/to/pattern.ext:123`
**Description:** [How this pattern is used in the design]

[Repeat for each pattern being followed]

## Tasks

Tasks are grouped by dependency. Complete tasks in each group before moving to the next.

### Setup and Foundation
- [ ] Create database schema in migrations/YYYY_MM_DD_feature_name.sql following existing migration pattern in migrations/
- [ ] Set up TypeScript types in src/types/feature.ts matching interface style from src/types/user.ts
- [ ] Add configuration keys to config/default.json following nested structure pattern

### Core Implementation
- [ ] Implement FeatureService class in src/services/FeatureService.ts following singleton pattern from src/services/UserService.ts
- [ ] Create API endpoints in src/routes/feature.ts following REST conventions from src/routes/user.ts
- [ ] Add authentication middleware to feature routes using src/middleware/auth.ts pattern

### Integration
- [ ] Integrate FeatureService with UserService in src/services/integration.ts following dependency injection pattern
- [ ] Update client API calls in client/src/api/feature.ts matching async/await pattern from client/src/api/user.ts
- [ ] Add React components in client/src/components/Feature/ following composition pattern from client/src/components/User/

### Testing and Validation
- [ ] Write unit tests in tests/unit/FeatureService.test.ts following Jest pattern from tests/unit/UserService.test.ts
- [ ] Add integration tests in tests/integration/feature.test.ts using test database setup from tests/setup.ts
- [ ] Create E2E tests in tests/e2e/feature.spec.ts following Playwright pattern from tests/e2e/user.spec.ts

### Documentation and Deployment
- [ ] Update API documentation in docs/api/feature.md following OpenAPI format from docs/api/user.md
- [ ] Add deployment steps to DEPLOYMENT.md if infrastructure changes needed
- [ ] Update CHANGELOG.md with feature description and breaking changes if any

## Additional Considerations

### Security
[Security concerns and mitigations]

### Performance
[Performance implications and optimizations]

### Error Handling
[Error scenarios and handling strategies]

### Future Enhancements
[Known limitations and future work]
```

## Task Writing Guidelines

**Each task must include:**
1. **What:** Clear action verb (Create, Implement, Add, Update, Write)
2. **Where:** Specific file path
3. **Context:** Reference to existing pattern/file to follow

**Good task examples:**
```markdown
- [ ] Create JWT auth middleware in src/auth/jwt.ts following existing session middleware pattern in src/auth/session.ts
- [ ] Implement WebSocket handler in src/websocket/notifications.ts matching event structure from src/websocket/chat.ts
- [ ] Add user profile API endpoint in src/routes/profile.ts following REST conventions from src/routes/user.ts:45-89
```

**Bad task examples:**
```markdown
- [ ] Add authentication          (too vague, no path, no context)
- [ ] Create src/auth/jwt.ts     (what goes in it? what pattern?)
- [ ] Implement middleware        (where? following what?)
```

## Task Grouping Strategy

**Group tasks by dependency, not by arbitrary phases.**

**Good grouping (dependency-based):**
```markdown
### Setup and Foundation
- [ ] Create database schema (nothing depends on rest of app)
- [ ] Set up types (independent of other code)

### Core Implementation (depends on Setup)
- [ ] Implement service (needs types)
- [ ] Create API routes (needs service)

### Integration (depends on Core)
- [ ] Integrate with existing services
- [ ] Update client code

### Testing (depends on Integration)
- [ ] Write tests
- [ ] Add E2E tests
```

**Bad grouping (arbitrary phases):**
```markdown
### Phase 1: Backend
- [ ] Create schema
- [ ] Implement service
- [ ] Write tests      (can't test without integration!)

### Phase 2: Frontend
- [ ] Update client
- [ ] Add components

### Phase 3: Testing
- [ ] E2E tests        (testing is sprinkled throughout)
```

**Dependency rules:**
- Tasks within a group can be done in parallel (if ralphy supports it)
- Tasks in later groups depend on earlier groups completing
- Typical dependency flow: Setup → Core → Integration → Testing → Documentation

## Writing Process

**REQUIRED: Create task tracker**

Use TaskCreate to create todos:
- Generate document structure
- Write Summary
- Write Architecture sections
- Document existing patterns
- Write task list with grouping
- Write Additional Considerations
- Generate Glossary
- Commit to git

Use TaskUpdate to track progress.

### Step 1: Generate Document Structure

Create file at `docs/design-plans/YYYY-MM-DD-<topic>.md` with sections:

```markdown
# [Feature Name] PRD

## Summary
<!-- Will be generated after body is written -->

## Definition of Done
[Copy confirmed Definition of Done from planning]

## Architecture
<!-- Will be filled next -->

## Existing Patterns
<!-- Will be documented next -->

## Tasks
<!-- Will be written after architecture -->

## Additional Considerations
<!-- Will be added at end -->

## Glossary
<!-- Will be generated after everything else -->
```

### Step 2: Write Summary

After Architecture and Tasks are complete, write 2-3 sentence summary:
- What's being built
- Why it matters
- Key approach

Keep it concise and high-level.

### Step 3: Write Architecture Sections

Based on validated design from brainstorming:

**Architecture > Overview:**
- High-level architecture description
- How components fit together
- Major design decisions

**Architecture > Components:**
- Key components and their responsibilities
- Interfaces between components
- Component relationships

**Architecture > Data Flow:**
- How data moves through the system
- Request/response flows
- State management approach

**Architecture > Technology Choices:**
- Technologies selected
- Rationale for each choice
- Alternatives considered (if relevant)

**Use concrete examples:** Show interface shapes, request/response formats, component relationships.

### Step 4: Document Existing Patterns

For each pattern the design follows:

```markdown
### [Pattern Name]
**Location:** `path/to/file.ext:line`
**Description:** [How this pattern applies to the design]
```

**How to find patterns:**
- Reference codebase-investigator findings from brainstorming
- Look up specific files mentioned in design
- Cite file:line for each pattern

**Example:**
```markdown
### REST API Conventions
**Location:** `src/routes/user.ts:12-45`
**Description:** All API routes follow Express Router pattern with async/await error handling middleware. This design adopts the same structure for consistency.

### Service Layer Pattern
**Location:** `src/services/UserService.ts:1-20`
**Description:** Services use singleton pattern with dependency injection via constructor. FeatureService will follow this exact pattern.
```

### Step 5: Write Task List

**For each dependency group:**

1. **Identify tasks needed**
   - Break design into concrete implementation steps
   - Each task = one file or coherent change
   - Include tests, docs, config changes

2. **Write detailed task descriptions**
   - Start with action verb (Create, Implement, Add, Update, Write)
   - Include specific file path
   - Reference existing pattern to follow
   - Add context from design (what goes in the file)

3. **Group by dependency**
   - Setup: Database, types, config (foundation)
   - Core: Services, APIs, main logic (builds on setup)
   - Integration: Connecting to existing code (needs core)
   - Testing: All test types (needs integration)
   - Documentation: Docs, deployment notes (final)

**Typical task categories:**
- Database/schema changes
- Type definitions
- Configuration
- Services/business logic
- API endpoints/routes
- Middleware
- Client-side integration
- UI components
- Unit tests
- Integration tests
- E2E tests
- Documentation
- Deployment steps

### Step 6: Write Additional Considerations

Document important cross-cutting concerns:

**Security:**
- Authentication/authorization requirements
- Input validation approach
- Security vulnerabilities mitigated
- Data protection measures

**Performance:**
- Performance implications
- Optimization strategies
- Caching approach
- Scalability considerations

**Error Handling:**
- Error scenarios
- Error response format
- Logging strategy
- Retry/fallback logic

**Future Enhancements:**
- Known limitations
- Potential improvements
- Features deferred to later
- Technical debt acknowledgment

**Keep it concise:** Bullet lists, not essays.

### Step 7: Generate Glossary

Create glossary of terms specific to this design:

```markdown
## Glossary

**Term 1:** Definition relevant to this design
**Term 2:** Definition relevant to this design
```

Include:
- Domain-specific terms
- Technical terms specific to this feature
- Acronyms used
- Ambiguous terms clarified

**Don't include:**
- Common programming terms (API, REST, etc.)
- Terms defined in project-level docs
- Obvious terms

### Step 8: Commit to Git

After document is complete:

```bash
git add docs/design-plans/YYYY-MM-DD-<topic>.md
git commit -m "$(cat <<'EOF'
Add [feature name] PRD

Ralphy-compatible PRD with design context and detailed task list.
Ready for task orchestration with ./ralphy.sh

Co-Authored-By: Claude Sonnet 4.5 <noreply@anthropic.com>
EOF
)"
```

## Output and Next Steps

After commit, announce:

```
PRD complete! Committed to `docs/design-plans/YYYY-MM-DD-<topic>.md`

Ready to start implementation with ralphy:

./ralphy.sh --prd docs/design-plans/YYYY-MM-DD-<topic>.md

Ralphy will execute tasks in dependency order, maintaining isolation between agents.
```

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Vague tasks | "Add authentication" | "Create JWT middleware in src/auth/jwt.ts following pattern from src/auth/session.ts" |
| Missing file paths | "Implement service" | "Implement FeatureService in src/services/FeatureService.ts" |
| No pattern reference | "Create API routes" | "Create routes in src/routes/feature.ts following REST conventions from src/routes/user.ts" |
| Arbitrary grouping | "Phase 1: Backend" | Group by dependency: "Setup → Core → Integration" |
| Tasks out of order | Tests before implementation | Setup → Core → Integration → Testing |
| Too high-level | "Build feature" | Break into 8-15 specific, actionable tasks |
| Too granular | 50+ tasks | Combine related changes, keep to 8-15 tasks |
| Missing context | Just file path | Include what goes in the file and pattern to follow |

## Key Principles

| Principle | Application |
|-----------|-------------|
| **Detailed tasks** | Each task includes what, where, and pattern to follow |
| **Dependency grouping** | Group tasks by dependency, not arbitrary phases |
| **Pattern references** | Every task cites existing code to follow |
| **Executable specificity** | Agent with zero codebase context can execute task |
| **Design context** | Architecture sections give agents the "why" |
| **Ralphy compatibility** | Output works directly with `./ralphy.sh --prd` |
| **Task tracking** | Use TaskCreate/TaskUpdate to track progress |
| **Complete documentation** | All sections filled, no TODOs left |
