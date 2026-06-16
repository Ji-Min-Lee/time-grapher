# Experiment Logging & Analysis Workflow

How to run a performance experiment on TimeGrapher, collect data, analyze it,
and record it in the deliverables. Follow these steps in order.

Concept references (in the project repo, not here):
- `docs/logging-design.md` — the logging facility (`ENABLE_LOGGING` / `--log`, CSV format)
- `docs/metrics-explained.md` — what a *frame* is, FPS/SPS/SPF, deadline, every graph panel
- `src/tools/README.md` — build & run scripts

---

## 1. Build with logging enabled

Logging is a compile-time switch (`--log`); release builds carry zero overhead.

```bash
# Raspberry Pi
./src/tools/run_timegrapher.sh all --log     # build (build-log/) + run

# Windows
.\src\tools\run_timegrapher.ps1 all --log
```

## 2. Run and capture

- Choose the input: **SIM** mode (synthetic watch beat) or **Mic** (live audio).
  On a headless / no-audio Pi, use **SIM** — the mic device may be null.
- Click **Start**, let it run for tens of seconds (watch the console
  `[NNNNNN]` summary lines confirming frames are recorded).
- **Close the window normally** (not `kill`/force-quit). The CSV is written once
  at shutdown; force-killing loses the data.

Output (per run) lands in `src/logs/`:
- `log_<timestamp>.csv`        — per-frame metrics, with a `#` header line:
  `# platform=... kernel=... host=... device=... git_commit=... sample_rate=...`
  (`git_commit` is injected by CMake from `git rev-parse --short HEAD` at build
  time, so each log self-identifies the exact build commit.)
- `log_<timestamp>_sys.csv`    — system metrics (RPi only: CPU/mem/temp/freq/throttle)

### Device identification (which Raspberry Pi)

Each Pi has `/home/whoami.json` with an `id` field (`rpi1` / `rpi2`). The logger
reads it at shutdown and writes `device=<id>` into the CSV `#` meta line, so each
log self-identifies its source unit (on Windows the file is absent →
`device=unknown`). `analyze_log.py` prints the device, so results can be sorted
by `rpi1` / `rpi2` without remembering which machine produced them.

`/home/whoami.json` example:
```json
{ "id": "rpi2", "label": "newer", "description": "external monitor",
  "memory_bandwidth_mibps": 12010 }
```

## 3. Organize into the experiment folder

Move the run's files into the matching experiment folder, separating by device
when comparing the two Pis, e.g.:

```
src/logs/EXP-02/log_<timestamp>.csv          # device shown in the # meta line
src/logs/EXP-02/log_<timestamp>_sys.csv
```

When tabulating in `experiment-results.md`, put the device (`rpi1`/`rpi2`, read
from the meta line) in the Platform column so runs from the two units are
distinguishable.

## 4. Analyze

```bash
python3 src/tools/analyze_log.py src/logs/EXP-02/log_<timestamp>.csv
```

Produces alongside the CSV:
- `log_<timestamp>.png`      — pipeline (latency / throughput / exec breakdown /
  per-frame e2e·wait·exec); the deadline line is auto-computed (`BG_SPF/BG_SPS`)
- `log_<timestamp>_sys.png`  — system metrics (when `_sys.csv` exists)

The console prints avg/max stats and the `Meta:` line (platform, sample rate).

## 5. Record in the deliverable

Edit `docs/milestone2/experiment-results.md`, in the relevant experiment (EXP-0X):

- Use a per-experiment run id like `E2-1`, `E2-2`, ... (the `E2` prefix scopes it
  to EXP-02 and avoids colliding with tactic ids `R1`/`T2` from
  `architectural-approaches.md`).
- Add **one row** to the narrow **Runs** table:
  `Run | Date | Platform | Rate | E2E avg/max (ms) | Role | git_commit | Detail`
  - **Platform / git_commit** come straight from the CSV `#` meta line
    (`device`, `git_commit`). For tag builds, write the commit and show the tag
    in parens, e.g. `6f741ec (tag macos_ex_t2)`.
  - **Role** = what the run is (e.g. `rpi2 baseline`, `E2-4 + T2 (DSP Offload)`).
    Reference tactic ids (R1/T2) to `architectural-approaches.md`.
  - `git_commit` makes each run reproducible — no separate provenance table needed.
- Add **one `<details>` block** under "Run details" with the full numbers and
  analysis (per-metric avg/max table, exec breakdown, throughput/backlog, system
  metrics, observations, conclusion, plot links). Keep the table narrow —
  everything else goes inside the collapsible block so the doc stays short.
- Update **Current Best** if the run improves on it.

## 6. Commit

- Commit the data (`src/logs/EXP-0X/*.csv`, `*.png`) and the doc together.
- All committed docs are in **English**.
- **Ask before `git push`** unless explicitly told to push.

---

## Metrics quick reference

| Field | Meaning |
|-------|---------|
| `samples` | samples processed in the frame (~SPF normally; higher = backlog) |
| `wait` | ① BG emit → FG start (queue + OS scheduling) |
| `exec` | ② FG processing (copy/sound/tg/ui/plot) |
| `total` | `wait + exec` (code-observable E2E per frame) |
| deadline | chunk period `BG_SPF / BG_SPS` (Win ≈10 ms, RPi ≈21 ms) |

`exec < deadline` = healthy. `wait`-dominated total = real-time/latency pressure.
See `docs/metrics-explained.md` for the full explanation.
