---
name: time-grapher
description: >-
  Context skill for the LG SW Architect Training Program TimeGrapher project.
  Provides project summary, milestone deliverables, TODO list, technical specs,
  and documentation conventions (English-only writing rule for all artifacts).
  Trigger when: "timegrapher", "time grapher", "assignment", "milestone",
  "architecture assignment", "watch", "acoustic", "raspberry pi assignment", "Qt assignment",
  "write doc", "create doc", "document",
  "workshop-followup", "architectural drivers", "risk assessment", "planned experiments",
  "architectural approaches", "project plan", "M1", "M2", "M3", "milestone 1", "milestone 2",
  "week1", "week2", "week3", "week4", "week5",
  "experiment", "experiment-results", "logging", "log analysis", "analyze_log",
  "latency measurement", "run_timegrapher", "--log", "EXP-01", "EXP-02",
  "issue", "kanban", "board", "roadmap", "github project",
  "sprint", "backlog", "todo", "in progress",
  "ADR", "architecture decision", "decision record".
metadata:
  version: 0.3.1
  last-updated-at: 2026-06-16
  language: en
  dependency-skills: []
---

# TimeGrapher Project Skill

> **LG Software Architecture Training Program × CMU MSE**  
> "From Tick to Trace: Real-Time Acoustic Analysis"

## Purpose

Provides the TimeGrapher project context to Claude for the LG SW Architect Training Program.
Loads the reference documents below when answering questions, planning, or reviewing to ensure accurate project-based responses.

## Documentation Rule — MUST FOLLOW

**English only.** Every artifact written or modified — documents, code, comments,
scripts, commit messages — MUST be in English. Do not write Korean in any file.
(This supersedes the earlier bilingual Korean/English convention; existing Korean
files do not need to be retranslated, but no new Korean should be added.)

**When writing a technical experiment document, ALWAYS use the template at [`assets/technical-experiment-template.md`](assets/technical-experiment-template.md) as the base structure. Do not create experiment docs from scratch.**

**When writing an Architecture Decision Record (ADR), ALWAYS use the template at [`assets/adr-template.md`](assets/adr-template.md) as the base structure. Do not create ADR docs from scratch.**

**When writing an architectural view document, ALWAYS use the template at [`assets/architectural-view-template.md`](assets/architectural-view-template.md) as the base structure. Do not create architectural view docs from scratch.**

ADR guidelines (from course reading):
- One decision per file; number ADRs sequentially (ADR-001, ADR-002, …)
- Keep it short (1–2 pages); use plain language
- List all consequences — positive and negative
- When a decision is superseded, keep the old ADR and link to the new one
- Store ADRs in version control alongside the architecture docs

> Violation: do not add Korean text to any file. Write everything in English.

---

## References

### Project

| Document | Contents |
|----------|----------|
| [Project Overview](references/project/overview.md) | Background, system architecture, quality attributes, tech stack |
| [Milestone Deliverables](references/project/milestones.md) | M1/M2/M3 deliverables and checkpoints |
| [Final Demo Grading Criteria](references/project/grading.md) | M3 채점표 — 8 areas, 200pts + 15pts bonus. Area별 배점 및 grader note 포함 |
| [TODO List](references/project/todo.md) | Weekly tasks + full schedule |
| [Conventions](references/project/conventions.md) | Documentation writing guide (language rule superseded — English only) |

### Workflow

| Document | Contents |
|----------|----------|
| [Experiment Logging & Analysis](references/workflow/experiment-logging.md) | How to run a performance experiment: build `--log`, capture, analyze with `analyze_log.py`, and record in `experiment-results.md` (narrow table + collapsible per-run details) |
| [GitHub Project Issue Management](references/workflow/github-project.md) | CRUD commands for the Kanban board (project #3), field IDs, Status options, title/label conventions |

### Design

| Document | Contents |
|----------|----------|
| [Architecture](references/design/skill-architecture.md) | Skill structure and module relationship diagram |
| [Module Contracts](references/design/skill-module-contracts.md) | Input/output/failure contracts |
| [Data Model](references/design/skill-data-model.md) | Project information data structure |
| [Dependency Map](references/design/skill-dependency-map.md) | Skill dependency and association relationships |

---

## Assets (assets/)

| File | Purpose |
|------|---------|
| `Time Grapher Project Plan (Draft).pdf` | Full requirements and deliverable spec (primary reference) |
| `LG 2026 Arch Kick Off Brief.pdf` | Kickoff slides |
| `TimeGrapher Equations_v0.docx.pdf` | Measurement calculation formulas |
| `TimeGrapher GUI Set Up Instructions.pdf` | Qt environment setup |
| `Witschi-Training-Course.pdf` | Watch measurement concepts (pp.14-19 required reading) |
| `Witschi Chronoscope X1 G3 Instruction Manual.pdf` | GUI display mode reference |
| `LG SW Architect Final Demo Grading Score Sheet and Ruberic.pdf` | Grading criteria |
| `TimeGrapher_v10.5_Student.zip` | Existing codebase |
| `technical-experiment-template.md` | Template for technical experiment documents (use this as base) |
| `adr-template.md` | Template for Architecture Decision Records (use this as base) |
| `issue-template.md` | Required fields + body templates for all issue types (EXP/FR/ARCH/Team/Doc/Bug/Done) |
| `architectural-view-template.md` | Template for architectural view documents (use this as base) |
