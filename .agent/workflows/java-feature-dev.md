---
description: High-Definition workflow for Java Spring Boot features. Enforces strict layering: Entity -> IRepo -> IDTO -> IService -> Test -> Impl -> Controller.
---

# Java Feature Development Workflow (Smart)

This workflow ensures you touch every layer of the architecture in the correct order.

## 1. Domain Modeling
**Goal**: Define the persistent state.
- **Skill**: `view_file .agent/skills/java/creating-java-entities/SKILL.md`
- **Output**: Pure `@Entity` class.

## 2. Data Access Layer
**Goal**: Define how to fetch the data.
- **Skill**: `view_file .agent/skills/java/creating-java-repositories/SKILL.md`
- **Output**: `JpaRepository` interface (and `QuerydslRepository` if complex).
- **Check**: Do NOT write business logic in the repo.

## 3. Service Contract & Data Transfer
**Goal**: Define the "What" before the "How".
- **Skill**: `view_file .agent/skills/java/creating-java-dtos/SKILL.md` (Service DTOs)
- **Skill**: `view_file .agent/skills/java/creating-java-services/SKILL.md` (Interface)
- **Output**: `Service` Interface and `ServiceDto` classes.

## 4. Test Driven Development (Red Phase)
**Goal**: Verify failure before success.
- **Skill**: `view_file .agent/skills/java/writing-java-tests/SKILL.md`
- **Action**: Write a test that mocks the Repository and asserts the Service logic.
- **Check**: Run test -> MUST FAIL.

## 5. Service Implementation (Green Phase)
**Goal**: Implement the business logic.
- **Skill**: `view_file .agent/skills/java/creating-java-services/SKILL.md` (Impl)
- **Skill**: `view_file .agent/skills/java/validating-java-data/SKILL.md` (If complex validation needed)
- **Action**: Implement `ServiceImpl`. Use `@Transactional`.
- **Check**: Run test -> MUST PASS.

## 6. API Layer (Controller & Spec)
**Goal**: Expose to the world.
- **Skill**: `view_file .agent/skills/java/creating-java-dtos/SKILL.md` (Controller DTOs)
- **Skill**: `view_file .agent/skills/java/creating-java-controllers/SKILL.md`
- **Action**: Create `@RestController`. Map Controller DTOs to Service DTOs.

## 7. Security & Documentation
**Goal**: Secure and Document.
- **Skill**: `view_file .agent/skills/java/securing-java-endpoints/SKILL.md` (`@PreAuthorize`)
- **Skill**: `view_file .agent/skills/java/documenting-java-code/SKILL.md` (Swagger)
- **Action**: Add Security annotations and Bilingual Swagger docs.
