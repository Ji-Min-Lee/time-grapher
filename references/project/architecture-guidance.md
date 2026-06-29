# Architecture Guidance — TimeGrapher

Reference document for QA hierarchy, architectural narrative pattern, and documentation anti-patterns.
Load this file when writing or reviewing ADRs, QA scenarios, tradeoff discussions, or presentation content.

---

## Quality Attribute Hierarchy — Canonical Project Framing

Accuracy is the **governing goal**, not one QA among equals. All other performance QAs are pursued *because* they are failure modes that corrupt accuracy:

```
Measurement Accuracy  ← governing goal (QAS-5)
├── Real-Time Performance (QAS-1)
│     A dropped audio block → missed beat → wrong Rate / Beat Error
│     → ADR-001 (DSP Offload Thread), EXP-01
├── Low Latency (QAS-2)
│     A stale display → user misreads current watch state
│     → ADR-001, EXP-02
└── Correctness (QAS-4)
      A formula error or false beat trigger → corrupts all output values
      → ADR-008 (WatchMath isolation), ADR-009 (FilterChain), EXP-04

Extensibility (QAS-3) — independent architectural driver
```

**Accuracy as tiebreaker** — three concrete examples where accuracy resolved a tradeoff:

| Decision | QA it pressured | Why accuracy won |
|----------|----------------|-----------------|
| 96 kHz over 48 kHz (ADR-003) | Performance (higher CPU cost) | Beat Error resolution halved at 48 kHz — unacceptable |
| WatchMath module isolation (ADR-008) | Simplicity (extra abstraction layer) | Formula errors untestable without isolation; error corrupts all output |
| FilterChain parameters exposed to user (ADR-009) | Usability (more complex UI) | Default parameters that degrade accuracy in one environment must be tunable |

When discussing tradeoffs, always connect them back to this hierarchy: "We chose X over Y because Y would have corrupted accuracy by …"

---

## Architectural Narrative Pattern

Every architectural claim should follow: **identified risk → decision → experiment validation**

Example (ADR-001 — Thread Separation):
> *Risk*: Qt event-loop bottleneck causes audio deadline misses (wait_ms = 420 ms). On constrained hardware like Raspberry Pi 5, this saturates one CPU core and causes backlog.
>
> *Decision*: Offload DSP to a dedicated thread (T2). We chose T2 over T3 (Full Pipeline Split) because T3 introduced three inter-stage queues and design complexity that exceeded M2 deadline feasibility.
>
> *Validated by*: EXP-02 — after T2, wait_ms dropped from 420 ms to 0.013 ms (×32,000). CPU load distributed across cores. 0 deadline misses, 0 backlog.

Apply the same structure to: ADR-003 (96 kHz), ADR-006 (Observer Pattern), ADR-007 (Downsampling), ADR-008 (WatchMath), ADR-009 (FilterChain).

**QA requirement rule**: QA scenarios describe the *problem* (goal + measurable response). They do NOT describe the solution, tactics, or experiments. Tactics belong in "Architectural Approaches". Experiments are separate documents.

---

## Anti-patterns — Do NOT Do These

Learned from M1/M2 course feedback.

### Documentation scope
- **No solutions in QA requirements** — QAS sections describe the goal and six-part decomposition only. Do not list tactics, design patterns, or experiment findings in a QAS.
- **No test reports in architecture docs** — test output belongs in CI, not in md files. Copying test reports into docs creates stale content.
- **No project history in behavior sections** — architecture view behavior sections show traces/state transitions that explain the structure. Sprint history, tab addition timelines, DSMs do not belong there.
- **No Dan's reference implementation in architecture views** — focus on YOUR architecture only.
- **No "fluff" from AI generation** — every sentence must earn its place. Verbose explanations of what a diagram already shows clearly are to be removed. When using AI to draft, explicitly instruct it to remove fluff, assume a well-informed reader, and stay concise.

### QA / requirements
- **Priority = H/M/L, not ranked 1–N** — a ranked list of 10 items hides the fact that items 1–6 are all High priority. Use H/M/L.
- **No provisional requirements** — if a response measure depends on an experiment, run the experiment first, then write the requirement with the validated number.

### ADR / ATAM
- **ADR Status = one word** — `Accepted`, `Proposed`, `Deprecated`, `Superseded`. No dates, no prose in the Status field.
- **ATAM docs are immutable snapshots** — mark them clearly: "This report captures the evaluation conducted on DATE and will not be updated." Do not treat ATAM files as living documents.
- **Cite [Bass21], not [Bass13]** — when referencing architecture tactics from the textbook, use `[Bass21]`.

### Kanban / project management
- **One Kanban board for the entire project** — not one per sprint or per week.
- **Every off-backlog card must have an assignee.**
- **Experiments must appear as Kanban tasks** with start date, end date, and assignee.
