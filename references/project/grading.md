# Final Demo Grading Criteria / 최종 데모 채점 기준

**Source**: `assets/Draft LG SW Architect Final Demo.pdf`  
**Applies to**: Milestone 3 Final Demo (2026-07-01)  
**Total**: 200pts + 15pts bonus

---

## Area 1 — Additional Real-Time Graphs & Diagnostic Displays (60pts)

Each graph/display must be demonstrated during the final presentation.

| Display | Points |
|---------|-------:|
| Watch-Position Testing | 5 |
| Trace Display | 5 |
| Rate and Amplitude Stability Over Time | 5 |
| Multi-Position Sequence Display | 5 |
| Beat-Noise Scope Display | 5 |
| Beat Error Display and Diagnostic Trace | 5 |
| Long-Term Performance Graph | 5 |
| Escapement Analyzer and Marker-Line Display | 5 |
| Time-Frequency Spectrogram Display | 5 |
| Waveform Comparison Display with Timing Markers | 5 |
| Scope Mode with Synchronized Sweep Display | 5 |
| Scope Function with Multiple Filter Views | 5 |
| **Total** | **60** |

**Grading scale**
- **Full**: feature is implemented, functional, and meaningfully integrated into the GUI
- **Partial**: feature is partially implemented, incomplete, unreliable, or poorly integrated
- **Zero**: feature is missing or non-functional

---

## Area 2 — System Enhancements & AI Feature (25pts)

| Item | Points |
|------|-------:|
| Sound Print enhancements improve event detection, readability, or interpretation | 8 |
| Rate/Scope enhancements improve usefulness, accuracy, navigation, or measurement clarity | 8 |
| Team-selected AI feature implemented as a useful proof of concept | 5 |
| Team explains what problem the AI feature addresses and how well it works | 4 |
| **Total** | **25** |

**Grading scale**: Excellent / Strong / Moderate / Minimal / None

---

## Area 3 — Quality Attribute Tradeoff Discussion (20pts)

Shown in presentation slides and demonstration.

| Item | Points |
|------|-------:|
| Clearly identifies the major quality attributes relevant to the project | 5 |
| Clearly explains tradeoffs among quality attributes | 5 |
| Shows that **accuracy** was treated as the highest-priority attribute in architecture and implementation | 5 |
| Explains what was actually achieved and what limitations remain | 5 |
| **Total** | **20** |

> **Key**: Grader evaluates team's understanding of architectural tradeoffs, especially prioritizing accuracy.

---

## Area 4 — Performance, Latency, and Correctness (25pts)

Shown in presentation slides and demonstration.

| Item | Points |
|------|-------:|
| Demonstrates real-time performance on the Raspberry Pi | 8 |
| Demonstrates low latency from signal capture to display/update | 6 |
| Demonstrates correctness of calculations, event detection, and displayed values | 6 |
| Presents evidence, measurements, experiments, or observations supporting these claims | 5 |
| **Total** | **25** |

**Real-time**: team clearly shows system operating in real time on the target platform  
**Low latency**: team clearly demonstrates low latency between capture, processing, and display  
**Correctness**: measurements, event detection, and displayed values are correct and consistent  
**Supporting evidence**: meaningful experiments, measurements, logs, comparisons, or demonstrations

---

## Area 5 — Extensibility of Architecture (20pts)

Shown in presentation slides.

| Item | Points |
|------|-------:|
| Architecture is modular and separates major concerns clearly | 6 |
| Architecture supports adding new measurements, filters, graphs, or displays with limited redesign | 6 |
| Team explains how the structure supports future requirements or enhancements | 4 |
| Code organization and interfaces make the system understandable and maintainable | 4 |
| **Total** | **20** |

---

## Area 6 — Remote UI / GUI Modifications (25pts)

| Item | Points |
|------|-------:|
| GUI improvements make the system easier to use and understand | 4 |
| System detects and responds appropriately to sensor or microphone unplug/replug events | 5 |
| UI layout uses screen space effectively (less-used controls in drop-downs or similar) | 4 |
| GUI supports beat-synchronized display of A and C events in same relative graph locations | 4 |
| GUI reduces or filters handling noise (tapping) while preserving useful signal features (A and C) | 4 |
| GUI provides clear overall system health, status, or measurement-readiness feedback | 4 |
| **Total** | **25** |

---

## Area 7 — Use of AI in Building the Software (15pts)

Shown in presentation slides.

| Item | Points |
|------|-------:|
| Team clearly explains how AI tools were used in development | 5 |
| Team shows thoughtful use of AI for design, coding, debugging, testing, documentation, or analysis | 5 |
| Team reflects on the strengths, limitations, and risks of AI-assisted development | 5 |
| **Total** | **15** |

> Grader evaluates **how** the team used AI, not just whether they mention it.

---

## Area 8 — Best User Interface (10pts)

| Item | Points |
|------|-------:|
| Comparative sponsor judgment: 1st=10, 2nd=8, 3rd=6, 4th=4, 5th=4 | 10 |
| **Total** | **10** |

---

## Grand Total

| Area | Points |
|------|-------:|
| 1. Additional Graphs & Displays | 60 |
| 2. System Enhancements & AI Feature | 25 |
| 3. QA Tradeoff Discussion | 20 |
| 4. Performance, Latency, Correctness | 25 |
| 5. Extensibility | 20 |
| 6. GUI Modifications | 25 |
| 7. Use of AI in Development | 15 |
| 8. Best UI | 10 |
| **Total** | **200** |

---

## Bonus — Additional Advanced Features (+15pts)

| Feature | Points |
|---------|-------:|
| Radar chart using measurements from multiple watch positions to assess overall watch health | 8 |
| Diagnosis/classification feature based on the readings | 7 |
| **Total** | **+15** |

**Radar Chart**: 8pts = implemented with meaningful multi-position data; 4–6pts = limited usefulness or integration; 1–3pts = partially implemented; 0pts = not demonstrated  
**Diagnosis/Classification**: 7pts = uses measured data to suggest watch condition or health; 4–5pts = somewhat useful but limited; 1–3pts = partially implemented; 0pts = not demonstrated
