# Skill Indexing Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** `.agent/skills/` 디렉토리 내의 모든 스킬 파일을 스캔하여 중앙 인덱스 파일(`SKILL_INDEX.md`)을 생성합니다. 이를 통해 AI가 전체 스킬 구조를 빠르고 정확하게 파악할 수 있게 합니다.

**Architecture:** `.agent/SKILL_INDEX.md` 파일을 생성하여 `Category > Skill Name > Description` 형식으로 정리합니다.

**Tech Stack:** Markdown, File System Scanning

---

### Task 1: Scan and Index Skills

**Files:**
- Create: `.agent/SKILL_INDEX.md`
- Read: `.agent/skills/**/SKILL.md`

**Step 1: Scan all skills**
- `.agent/skills` 하위의 모든 `SKILL.md` 파일을 찾습니다.
- 각 파일에서 `name`과 `description` (YAML frontmatter)을 추출합니다.
- 디렉토리 구조를 기반으로 카테고리를 분류합니다 (예: `common`, `java`, `react`).

**Step 2: Generate Index Content**
Create the content in the following format:

```markdown
# Superpowers Skill Index

This file is auto-generated. It lists all available skills for the agent.

## Common
- **planning**: Creates comprehensive implementation plans...
- **brainstorming**: ...

## Java
- **creating-java-entities**: ...
- ...

## React
- ...
```

**Step 3: Write Index File**
- Save the content to `.agent/SKILL_INDEX.md`.

**Step 4: Verify**
- Check if `.agent/SKILL_INDEX.md` exists and contains the list of skills.

---
