---
description: Standard Development Workflow following Superpowers methodology
---

# 1. Brainstorming (기획)
[브레인스토밍 스킬]을 사용하여 사용자의 요구사항을 구체화하고 의도를 파악합니다.
- 사용 도구: `view_file .agent/skills/common/brainstorming/SKILL.md`
- 목표: 명확한 요구사항 정의서 도출

# 2. Planning (계획 수립)
확정된 요구사항을 바탕으로 [Planning 스킬]을 사용하여 상세 구현 계획을 수립합니다.
- 사용 도구: `view_file .agent/skills/common/planning/SKILL.md`
- 목표: 작은 단위로 쪼개진 `task.md` 생성

# 3. Environment Setup (환경 설정)
// turbo
프로젝트 상태를 확인하고 필요한 경우 [Git Worktree 스킬]을 사용하여 작업 환경을 격리합니다.
- 명령어: `git status`
- 권장 참조: `view_file .agent/skills/common/using-git-worktrees/SKILL.md`

# 4. Implementation (구현 - Loop)
Language-Specific Workflows를 호출하여 개발을 진행합니다.
- Java: `view_file .agent/workflows/java-feature-dev.md`
- React: `view_file .agent/workflows/react-feature-dev.md`

또는 공통 TDD 스킬 사용:
- 사용 도구: `view_file .agent/skills/common/test-driven-development/SKILL.md`

# 5. Review & Verification (검증)
[Review 스킬]을 사용하여 작성된 코드를 검토하고, 테스트를 수행합니다.
- 사용 도구: `view_file .agent/skills/common/reviewing-code/SKILL.md`
- 권장 명령어: `npm test` (또는 해당 프로젝트의 테스트 명령)
