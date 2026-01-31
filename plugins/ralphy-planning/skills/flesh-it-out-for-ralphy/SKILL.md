---
name: flesh-it-out-for-ralphy
description: Use when user has rough idea that needs refinement before full planning - uses asking-clarifying-questions to strengthen ideas and resolve contradictions, preparing for start-ralphy-plan
---

# Flesh It Out For Ralphy

## Overview

Transform rough, general ideas into clear, specific concepts ready for full design planning. Acts as friendly but honest critic to strengthen ideas before investing in complete design process.

**Core principle:** Clarify → Strengthen → Prepare for planning.

**Announce at start:** "I'm using the flesh-it-out-for-ralphy skill to help refine your idea before we create a full plan."

## When to Use

**Use this skill when:**
- User has general idea but hasn't thought through details
- Idea contains contradictions or ambiguities
- Requirements are vague or underspecified
- User wants quick feedback before committing to full planning

**Don't use this skill when:**
- User has clear, detailed requirements (go straight to start-ralphy-plan)
- User has already done significant planning work
- Idea is already specific and well-formed

## Quick Reference

| Phase | Activities | Tool |
|-------|-----------|------|
| **1. Capture** | Get user's rough idea | Open-ended questions |
| **2. Clarify** | Use asking-clarifying-questions skill | Subagents + AskUserQuestion |
| **3. Handoff** | Direct to start-ralphy-plan | Announce next step |

## The Process

**REQUIRED: Create task tracker**

Use TaskCreate to create todos:
- Capture rough idea
- Clarify and strengthen (using asking-clarifying-questions)
- Hand off to start-ralphy-plan

Use TaskUpdate to track progress.

### Phase 1: Capture Rough Idea

Use TaskUpdate to mark "Capture rough idea" as in_progress.

**If user hasn't provided content yet:**

Ask them for it:

"I'm here to help refine your idea into something ready for planning. Please share:

- What you're thinking about building
- Why you want to build it
- Any specific concerns or questions you have
- Anything else on your mind about this

Don't worry about being complete or polished - that's what we'll work on together."

**If user already provided rough idea:**

Acknowledge what they've shared:

"I see you're thinking about [brief summary]. Let me help clarify and strengthen this before we move to full planning."

Mark "Capture rough idea" as completed.

### Phase 2: Clarify and Strengthen

Use TaskUpdate to mark "Clarify and strengthen" as in_progress.

**REQUIRED SUB-SKILL:** Use ed3d-plan-and-execute:asking-clarifying-questions

Announce: "I'm using the asking-clarifying-questions skill to help strengthen your idea."

**The clarification skill will:**
- Identify contradictions and resolve them
- Tease out ambiguities
- Question vague statements
- Surface hidden assumptions
- Help make the idea clear and strong

**Your role during clarification:**
- Act as friendly but honest critic
- Point out weaknesses without judgment
- Ask "what about X?" questions
- Help user think through implications
- Don't let contradictions pass

**Output:** Clear, specific idea ready for full planning.

Mark "Clarify and strengthen" as completed when idea is strong.

### Phase 3: Hand Off to Planning

Use TaskUpdate to mark "Hand off to start-ralphy-plan" as in_progress.

**Announce next step:**

```
Your idea is now clear and ready for full planning!

Next step: Use the start-ralphy-plan skill to:
1. Gather complete context
2. Further clarify requirements (if needed)
3. Explore design alternatives through brainstorming
4. Create ralphy-compatible PRD with detailed tasks

Run this command:

/ralphy-planning:start-ralphy-plan
```

Mark "Hand off to start-ralphy-plan" as completed.

## Key Differences from Full Planning

| Aspect | Flesh It Out | Start Ralphy Plan |
|--------|-------------|-------------------|
| **Depth** | Surface-level clarity | Complete design |
| **Duration** | 5-10 minutes | 20-60 minutes |
| **Output** | Clear concept | Ralphy-compatible PRD |
| **Research** | Minimal | Extensive (codebase + internet) |
| **Brainstorming** | No formal brainstorming | Full 3-phase brainstorming |
| **Documentation** | None | Committed PRD file |

## Example Flow

**User starts with rough idea:**
```
User: "I want to add notifications to the app"
```

**Flesh it out clarifies:**
```
Assistant: What kind of notifications?
User: Email and in-app

Assistant: For what events?
User: New messages, mentions, status updates

Assistant: Who receives these notifications?
User: All logged-in users

Assistant: What happens when user is offline?
User: (pauses) Hmm, I hadn't thought about that...
```

**Result after clarification:**
- Notifications for: new messages, mentions, status updates
- Delivery: Email (offline) + in-app (online)
- Recipients: All logged-in users
- Edge case identified: Offline notification queuing

**Hand off to planning:**
```
Your idea is now clear\! Ready for /ralphy-planning:start-ralphy-plan
```

## Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Skipping clarification | Rough idea stays rough | Always use asking-clarifying-questions skill |
| Being too accepting | Contradictions pass through | Act as critical friend - point out issues |
| Going too deep | Spending 30+ minutes | Keep it surface-level, save depth for full planning |
| Not handing off | User doesn't know next step | Always provide /ralphy-planning:start-ralphy-plan command |

## Key Principles

| Principle | Application |
|-----------|-------------|
| **Quick refinement** | 5-10 minutes max, not full planning session |
| **Honest feedback** | Point out contradictions and gaps |
| **Clarification focus** | Use asking-clarifying-questions skill |
| **Clear handoff** | Direct to start-ralphy-plan when done |
| **Task tracking** | Use TaskCreate/TaskUpdate to track progress |
