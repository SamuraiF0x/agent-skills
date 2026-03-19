---
name: refactor
description: Refactor existing code for readability, maintainability, and structure without changing behavior. Use when files are too large, responsibilities are mixed, or separation of concerns is weak.
argument-hint: "[target file or scope]"
---

# Refactor

Refactor code with strict behavior parity and clear separation of concerns.

## When to Use This Skill

- A file is hard to read or maintain.
- UI, state, side effects, and business logic are mixed together.
- A React or React Native component is too large and needs decomposition.
- Type safety is weak, for example in any-heavy code.

## Non-negotiable Constraints

- Do not change runtime behavior.
- Keep naming clear and intention-revealing.
- Reduce nesting and complexity.
- Improve type safety and avoid introducing any.
- Keep each refactored file under 300 lines when practical.
- Follow existing project conventions and style.

## Refactor Procedure

1. Baseline analysis
   - Read the implementation end-to-end.
   - Identify responsibilities: UI rendering, state, side effects, pure logic, and types.
   - Note external interfaces that must remain stable, such as props, exports, hook contracts, and side-effect timing.

2. Design target structure
   - Propose a split with clear boundaries:
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

3. Extract in safe order
   - Move type definitions first.
   - Extract pure utility functions next.
   - Extract custom hooks for reusable state and effects.
   - Split UI into smaller focused components.
   - Keep imports and exports explicit and minimal.
   - Add clear documentation to top of each file.

4. Preserve behavior
   - Keep public API unchanged unless explicitly requested.
   - Preserve defaults, conditionals, and edge-case handling.
   - Avoid accidental behavior changes during cleanup.

5. Validate
   - Run available tests and lint/type checks.
   - If no tests exist, perform focused reasoning checks on side effects, data flow, and render output.
   - Confirm no regressions in integration points.

## Output Format

1. Suggested folder structure
2. Refactored code split into files
3. Brief explanation of key improvements

## React and React Native Notes

- Prefer small presentational components with narrow props.
- Isolate event handlers and effectful logic in hooks.
- Keep utility modules framework-agnostic where possible.
- Use explicit TypeScript types for component props and hook returns.
- Introduce Zod only when runtime validation is actually needed.
