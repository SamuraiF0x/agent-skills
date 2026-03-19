---
name: improve-arch
description: Follow-up to the refactor skill. Explore the surrounding codebase to find deep-module architecture improvements that increase testability and reduce coupling.
argument-hint: "[scope from refactor or module cluster]"
---

# Improve Architecture

Use this skill after `refactor` to move from local cleanup to architectural deepening.

A deep module (John Ousterhout, A Philosophy of Software Design) exposes a small interface while hiding substantial complexity. Deep modules improve testability, reduce integration risk, and make codebases easier for humans and AI agents to navigate.

## Prerequisite

- The `refactor` skill has already been run for the target scope.
- You have a handoff from `refactor` with:
  - changed files and stable interfaces
  - known seam points and coupling hotspots
  - test gaps or brittle tests

## Dependency Categories

Use these categories when describing coupling:

1. Data shape coupling: Modules share low-level types or data contracts.
2. Temporal coupling: Call order or lifecycle timing is critical.
3. Control-flow coupling: A caller must orchestrate many steps correctly.
4. Infrastructure coupling: Domain logic is entangled with IO/framework/runtime concerns.

## Process

### 1. Anchor on refactor handoff

- Summarize what `refactor` changed and what remained stable.
- Capture unresolved pain points that still require architectural work.

### 2. Explore the codebase

Use the Agent tool with `subagent_type=Explore` to inspect the surrounding system naturally.
Do not force rigid heuristics. Friction is the signal.

Look for:

- concepts requiring context switching across many tiny files
- shallow modules whose interface is almost as complex as implementation
- pure helpers extracted for testability while real failures occur in orchestration seams
- tightly coupled modules that create integration risk
- untested behavior that is difficult to verify at a boundary

### 3. Present architecture candidates

Provide a numbered list of deepening opportunities. For each candidate include:

- Cluster: modules and concepts involved
- Why coupled: concrete coupling evidence
- Dependency category: one or more categories above
- Test impact: brittle tests that can be replaced with boundary tests

Do not propose interfaces yet.
Then ask: "Which candidate should we design?"

### 4. Frame the problem space

For the selected candidate, provide a user-facing framing with:

- interface constraints that must hold
- dependencies a deepened module must manage
- a rough illustrative code sketch (not the final proposal)

Immediately continue to Step 5 while the user reads.

### 5. Design multiple interfaces in parallel

Spawn 3 or more sub-agents in parallel using the Agent tool.
Each sub-agent must produce a radically different interface.

Use one brief per sub-agent including:

- relevant file paths and coupling facts
- dependency category focus
- complexity to hide behind the new boundary

Assign constraints:

- Agent 1: Minimize interface (1-3 entry points)
- Agent 2: Maximize flexibility (extension-friendly)
- Agent 3: Optimize default path for the most common caller
- Agent 4 (when relevant): Ports and adapters for cross-boundary dependencies

Each sub-agent output must include:

1. Interface signature (types, methods, parameters)
2. Caller usage example
3. Complexity hidden internally
4. Dependency strategy
5. Trade-offs

Present designs sequentially, compare in prose, then give a strong recommendation.
If a hybrid is best, define it explicitly.

### 6. Select final direction

Have the user pick one design (or accept your recommendation).

### 7. Create implementation RFC issue

Create a GitHub issue with `gh issue create` and share the URL.
Do not ask the user to approve the issue body before creation.

Use this template:

```md
# [RFC] Deepen module: <candidate name>

## Context
- Scope from refactor:
- Current coupling evidence:
- Why current shape is shallow:

## Goals
- Increase boundary-level testability
- Reduce coupling category/categories:
- Keep external behavior stable

## Proposed Interface
- Entry points:
- Input/output contracts:
- Dependency strategy:

## Hidden Complexity
- What moves behind the boundary:
- Internal orchestration responsibilities:

## Migration Plan
1. Introduce new boundary behind existing interface.
2. Move orchestration and side-effect coordination inward.
3. Replace seam-heavy tests with boundary tests.
4. Remove obsolete glue modules.

## Test Plan
- Boundary tests to add:
- Existing tests to remove or simplify:
- Regression checks:

## Risks and Mitigations
- Risk:
- Mitigation:

## Acceptance Criteria
- [ ] Public behavior unchanged
- [ ] New boundary covers key integration paths
- [ ] Reduced cross-module orchestration in callers
- [ ] Tests validate behavior at boundary

## Out of Scope
- Non-related rewrites
- New product behavior
```

## Output Format

1. Candidate list with coupling and test impact
2. Interface options and recommendation
3. Created GitHub issue URL
