# Superpowers Skill Index

This file is auto-generated. It lists all available skills for the agent.

## Common (Generals)
- **brainstorming**: Use when you need to generate ideas, architecture, or solutions before implementation. Can create specific documents like PRD or Architecture Decision Records.
- **brand-identity**: A single source of truth for brand guidelines, design tokens, technology choices, and voice/tone.
- **configuring-persona**: Dynamically loads persona definitions, instructions, and styles from the global prompt armory.
- **creating-skills**: Use when creating new skills or updating existing ones. Follows the Superpowers standard structure.

- **dispatching-parallel-agents**: Use when multiple independent tasks need to be executed in parallel sessions to save time.
- **executing-plans**: Use when executing a multi-step implementation plan (parallel session mode).
- **finishing-a-development-branch**: Use when all tasks in a branch/plan are complete. Runs final verification and prepares for merge.
- **generating-workflows**: Creates new workflow files (.md) in .agent/workflows for repeatable processes.
- **planning**: Creates comprehensive implementation plans with bite-sized tasks. Use when requirements are clear but code has not started.
- **receiving-code-review**: Use when you need to act on code review feedback provided by a reviewer.
- **requesting-code-review**: Use when you have finished implementation and need a code review from a subagent or the user.
- **reviewing-code**: Use when you need to review code changes against specs and quality standards.
- **subagent-driven-development**: Use when executing implementation plans with independent tasks in the current session (sequential subagents).
- **summarizing-sessions**: Analyzes conversation history to generate structured session reports and summaries.
- **systematic-debugging**: Use when encountering any bug, test failure, or unexpected behavior. follow a strict diagnose-fix-verify loop.
- **test-driven-development**: Use before writing implementation code. Write failing test -> make it pass -> refactor.
- **using-git-worktrees**: Use when creating isolated environments for feature development or plan execution.
- **using-superpowers**: The core protocol. Requires checking skills before ANY response.
- **verification-before-completion**: Use before asserting a task is done. Run tests and commands to prove it works.
- **writing-plans**: Use to generate detailed implementation plans with step-by-step tasks.
- **writing-skills**: Use when authoring or editing skill files. Enforces formatting and best practices.

## Java (Backend)
- **configuring-java-beans**: Generates Spring `@Configuration` classes and manages Application Properties.
- **creating-java-controllers**: Generates Spring `@RestController` classes enforcing DTO usage and service delegation.
- **creating-java-dtos**: Generates Java DTOs enforcing Two-Layer pattern and Bean Validation.
- **creating-java-entities**: Generates Spring JPA Entities ensuring pure domain state and auditing.
- **creating-java-repositories**: Generates Spring Data JPA Repositories and QueryDSL Custom Repositories.
- **creating-java-services**: Generates Java Spring Services using Interface-Implementation pattern.
- **documenting-java-code**: Enforces Swagger/OpenAPI documentation standards with bilingual descriptions.
- **implementing-java-async**: Implements `@Async` tasks and `@Scheduled` jobs with strict tracking.
- **implementing-java-pagination**: Implements Django-style pagination with `PageResponse` and sort validation.
- **securing-java-endpoints**: Implements Spring Security, JWT authentication, and method-level security.
- **validating-java-data**: Implements domain validation using `@Component` Validators and Bean Validation.
- **writing-java-tests**: Generates Java Unit Tests following strict TDD and Given-When-Then standards.

## React (Frontend)

- **creating-react-api-modules**: Generates Type-Safe API modules for React returning QueryOptions.
- **creating-react-components**: Generates React Function Components focusing on rendering only.
- **creating-react-hooks**: Generates Custom React Hooks for business logic orchestration.
- **creating-react-types**: Generates strict TypeScript types/interfaces and Enums.
- **creating-react-utils**: Generates pure utility functions for formatting and validation.
- **managing-react-form-state**: Manages complex form state using `useReducer`.
- **managing-react-global-state**: Manages global client-side state using Redux Toolkit or Context.

## Learning (Methodology)
- **deconstructing-knowledge**: Breaks down complex topics or keywords into fundamental "atomic" units using First Principles thinking.
- **evolving-skills**: Dynamically updates and refines the agent's skills based on proven best practices.
- **mapping-curriculum**: Organizes decomposed knowledge into a logical "Base to Top" learning roadmap.
- **pure-standards**: A living repository of high-end architectural standards and "sexy" code patterns.
- **testing-mastery**: Verifies understanding using the Feynman Technique and active recall.

