---
description: Start full design planning workflow for ralphy PRD
allowed-tools: Read, Grep, Glob, Bash, Edit, Write, Task, AskUserQuestion, TaskCreate, TaskUpdate, TaskList, TaskGet, WebFetch, WebSearch
---

# Ralphy Planning

Use the `ralphy-planning:start-ralphy-plan` skill to guide the user through the complete design process.

This includes:
1. Context Gathering - Collect requirements, constraints, goals
2. Clarification - Disambiguate requirements
3. Definition of Done - Confirm success criteria
4. Brainstorming - Explore alternatives, validate design
5. PRD Documentation - Create ralphy-compatible PRD
6. Ralphy Handoff - Provide execution command

Output will be a ralphy-compatible PRD at `docs/design-plans/YYYY-MM-DD-<topic>.md`.
