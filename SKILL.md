---
name: time-grapher
description: >-
  Context skill for the LG SW Architect Training Program TimeGrapher project.
  Provides project summary, milestone deliverables, TODO list, technical specs,
  documentation conventions (English-only writing rule for all artifacts),
  QA hierarchy, architectural narrative patterns, and M1/M2 anti-patterns.
  Trigger when: "timegrapher", "time grapher", "assignment", "milestone",
  "architecture assignment", "watch", "acoustic", "raspberry pi assignment", "Qt assignment",
  "write doc", "create doc", "document", "presentation", "slide", "grading",
  "workshop-followup", "architectural drivers", "risk assessment", "planned experiments",
  "architectural approaches", "project plan", "M1", "M2", "M3", "milestone 1", "milestone 2",
  "week1", "week2", "week3", "week4", "week5",
  "experiment", "experiment-results", "logging", "log analysis", "analyze_log",
  "latency measurement", "run_timegrapher", "--log", "EXP-01", "EXP-02",
  "issue", "kanban", "board", "roadmap", "github project",
  "sprint", "backlog", "todo", "in progress",
  "ADR", "architecture decision", "decision record",
  "QA", "quality attribute", "accuracy", "tradeoff", "ATAM", "AI usage", "ai-usage".
metadata:
  version: 0.4.1
  last-updated-at: 2026-06-30
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
- **Status field**: one word only — `Proposed`, `Accepted`, `Deprecated`, or `Superseded`. No dates, no extended prose. Git history records the rest.

> Violation: do not add Korean text to any file. Write everything in English.

---

## References

### Project

| Document | Contents |
|----------|----------|
| [Project Overview](references/project/overview.md) | Background, system architecture, quality attributes, tech stack |
| [Milestone Deliverables](references/project/milestones.md) | M1/M2/M3 deliverables and checkpoints |
| [Final Demo Grading Criteria](references/project/grading.md) | M3 grading rubric — 8 areas, 200pts + 15pts bonus. Per-area points and grader notes |
| [TODO List](references/project/todo.md) | Weekly tasks + full schedule |
| [Conventions](references/project/conventions.md) | Documentation writing guide (language rule superseded — English only) |
| [Architecture Guidance](references/project/architecture-guidance.md) | QA hierarchy (Accuracy-first), risk→decision→experiment pattern, M1/M2 anti-patterns |

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

## Use Cases

### UC-1: Writing a Document (QAS, ADR, Experiment, etc.)

**When**: User asks to write or review any project document — requirements, ADR, experiment report, ATAM section, lessons-learned, etc.

**Load**:
- `references/project/milestones.md` — check which milestone the document belongs to and what the deliverable spec requires
- `references/project/architecture-guidance.md` — apply QA hierarchy (accuracy-first), risk→decision→experiment pattern, and anti-patterns
- Relevant template from `assets/` — `adr-template.md`, `technical-experiment-template.md`, or `architectural-view-template.md`
- Course feedback embedded in `architecture-guidance.md` (Anti-patterns section) — enforce M1/M2 corrections

**Key rules**:
- QA scenarios describe the *problem* only — no tactics, no solutions, no experiment findings inside a QAS
- ADR Status = one word; no prose in the Status field
- ATAM docs must be marked as immutable snapshots with a date header
- QA priority = H/M/L, not ranked 1–N
- No "fluff" — every sentence must earn its place; instruct AI to assume a well-informed reader

---

### UC-2: Writing an Architectural View

**When**: User asks to write or revise any architectural view document — Module, C&C, Layered, Deployment, Decomposition, or any other view type.

**Load**:
- `references/project/milestones.md` — confirm view is required for the current milestone
- `references/project/architecture-guidance.md` — apply anti-patterns (no Dan's reference impl, no project history in behavior section, no DSM unless justified, no verbose AI-generated behavior prose)
- `assets/architectural-view-template.md` — use as structural base; do not deviate from the section order
- `assets/TimeGrapher/` source files — read actual implementation to ground the view in real code (class names, thread structure, signal/slot connections)
- `references/project/grading.md` — confirm what graders evaluate in extensibility and architecture sections (Area 3, 5)

**Key rules**:
- Diagrams come first; behavior prose only adds what the diagram cannot show
- Legend shows element *types* only — no actual names in the legend
- Behavior section = traces / state transitions that explain structural decisions. Not sprint history, not test reports, not DSMs
- Do not show Dan's reference implementation unless there is an explicit stakeholder reason

---

### UC-3: Naming an Architectural View

**When**: User asks what to name a view, or whether an existing name is appropriate.

**Naming conventions from course feedback**:

| View type | Correct naming pattern | Examples |
|-----------|----------------------|---------|
| Module decomposition | `<Subject> Module Decomposition View` | `Graph Tab Module Decomposition View` |
| Module uses | `<Subject> Module Uses View` | `IAudioSource Module Uses View` |
| Layered | `Layered View` or `Layered and Module Decomposition View` | Do not include the number of layers or "Allowed-to-Use" in the name |
| C&C | `<Subject> C&C View` | `DSP Pipeline Thread C&C View` |
| Deployment | `Deployment View` | Do not call it "Build-Deploy Pipeline" unless the audience is specifically DevOps |

**Anti-pattern names to avoid**:
- `Layered View: 4-Layer Allowed-to-Use` → drop the layer count and relation type from the name
- `Decomposition View: Graph Tab` → "Decomposition" implies module–submodule; rename to `Graph Tab Module Uses View` if showing uses relations
- `Deployment View: Build-Deploy Pipeline` → deployment view should focus on hardware/runtime topology, not the CI pipeline

---

### UC-4: Code Development

**When**: User asks to implement a feature, fix a bug, add a new graph tab, extend the DSP pipeline, or write tests.

**Load**:
- `references/project/overview.md` — tech stack, operating modes (Live / Playback / Sim), hardware constraints (Raspberry Pi 5, 96 kHz ALSA deadline)
- `references/project/architecture-guidance.md` — QA hierarchy: accuracy is the governing goal; any implementation decision that degrades beat detection or measurement correctness is unacceptable regardless of other benefits
- `assets/TimeGrapher/` source files — understand existing class structure before adding code
- `assets/TimeGrapher Equations_v0.docx.pdf` — reference for Rate, Amplitude, Beat Error formulas

**Key rules**:
- New graph tabs must implement `BaseGraphTab` (ADR-006 Observer Pattern) — do not wire signals directly from `MainWindow`
- DSP logic must stay in the DSP thread (T2) — no audio processing on the Qt main thread
- Measurement formulas must go through `WatchMath` (ADR-008) — do not inline calculations in UI code
- Sample rate is 96 kHz; all timing calculations must use this as the baseline unless overridden by the user's BPH setting
- AGC must be disabled (verify in AlsaMixer before any audio capture test)

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
