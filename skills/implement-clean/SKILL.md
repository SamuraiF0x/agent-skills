---
name: implement-clean
description: Implement new features and updates using the same structural rules as refactor from the start, so cleanup is built in instead of deferred.
argument-hint: "[feature scope or target module]"
---

# Implement Clean

Use this skill by default when adding new features or updating existing behavior.

This is the proactive version of `refactor`: apply the same readability, maintainability, and separation-of-concerns rules while implementing, so later refactors are smaller and less frequent.

## When to Use This Skill

- You are adding a new feature.
- You are updating existing behavior.
- You are touching a large or mixed-responsibility module and want to avoid creating more debt.
- You want changes to be production-ready without a follow-up cleanup pass.

## Non-negotiable Constraints

- Keep existing behavior unchanged outside the requested feature scope.
- Keep naming clear and intention-revealing.
- Reduce nesting and complexity.
- Improve type safety and avoid introducing any.
- Keep each touched file under 300 lines when practical.
- Follow existing project conventions and style.

## Implementation Procedure

1. Scope and safety baseline
   - Define the requested behavior change and explicit non-goals.
   - Identify existing interfaces that must remain stable, such as props, exports, hook contracts, API payloads, and side-effect timing.
   - Mark what can change vs what must remain untouched.

2. Design target structure before coding
   - Propose a clean split when needed:
     - components/
     - hooks/
     - utils/
     - types/
     - constants/
   - Keep responsibilities explicit:
     - components: presentation
     - hooks: stateful orchestration and side-effect coordination
     - utils: pure reusable logic
     - types: shared interfaces and type helpers
     - constants: shared configuration, feature flags, and magic numbers

3. Implement feature in safe order
   - Add or update type definitions first.
   - Add pure utility logic next.
   - Add or update hooks for state/effects.
   - Add or update UI components with narrow props.
   - Keep imports and exports explicit and minimal.
   - Add clear documentation at the top of each new file.

4. Preserve surrounding behavior
   - Keep public APIs unchanged unless the feature requires a deliberate interface change.
   - Preserve defaults and edge-case handling outside requested scope.
   - Avoid opportunistic rewrites that are not required for the feature.

5. Validate and guard regressions
   - Run available tests and lint/type checks.
   - Add or update tests for the new feature behavior.
   - If test coverage is limited, do focused reasoning checks on side effects, data flow, and render output.

## Output Format

1. Feature scope summary (what changed and what stayed stable)
2. Suggested folder/file structure for touched code
3. Implemented code split by file
4. Validation summary (tests/checks and regression notes)

## React and React Native Notes

- Prefer small presentational components with narrow props.
- Isolate event handlers and effectful logic in hooks.
- Keep utility modules framework-agnostic where possible.
- Use explicit TypeScript types for component props and hook returns.
- Introduce Zod only when runtime validation is actually needed.