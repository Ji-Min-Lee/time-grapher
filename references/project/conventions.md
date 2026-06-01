# TimeGrapher — Documentation Conventions

## Bilingual Writing Guide (한/영 병기)

All project documentation under `docs/` must be written in **both Korean and English**.

---

### File Header

Every document must open with a bilingual title and metadata block:

```markdown
# 한국어 제목 / English Title

> **작성일 / Date**: YYYY-MM-DD  
> **출처 / Source**: (reference if applicable)
```

---

### Section Headers

Write section headers in both languages, separated by ` / `:

```markdown
## 1. 한국어 섹션 제목 / English Section Title
```

---

### Body Text

Within each section, present Korean first, then English, each under its own **bold label**:

```markdown
**한국어**

한국어 본문 내용을 여기에 씁니다.

**English**

Write the English body text here.
```

> Always write Korean first, then English.

---

### Tables

Use a single bilingual header row. Separate Korean and English with ` / ` inside each cell:

```markdown
| 항목 / Item | 설명 / Description | 단위 / Unit |
|-------------|-------------------|-------------|
| 레이트 / Rate | 하루 오차 / Daily deviation | s/d |
```

---

### Inline Terms

For technical terms introduced for the first time, show the Korean term followed by the English term in parentheses, or vice versa, depending on which is primary:

```markdown
탈진기(escapement) / 진폭(Amplitude) / 박동 오류(Beat Error)
```

---

### Code Blocks and Diagrams

No translation needed inside code fences or Mermaid diagrams. Use English identifiers and add bilingual comments only if the logic needs explanation:

```cpp
// 박동 감지 / Beat detection
detectBeat(signal);
```

---

### Reference — Existing Example

`docs/week1/kickoff-workshop/domain-knowledge.md` follows this convention and can be used as a reference template.

---

### Checklist Before Committing a Doc

- [ ] Title uses `한국어 제목 / English Title` format
- [ ] Every `##` section header has both languages
- [ ] Each section has a `**한국어**` block followed by an `**English**` block
- [ ] Tables use bilingual header cells
- [ ] No Korean-only or English-only paragraphs in the body
