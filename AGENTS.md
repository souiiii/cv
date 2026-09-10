# CV Mid-Semester Project Instructions

## Purpose

This repository is for **7th-semester IT Computer Vision midsem preparation**. Optimize for the actual paper, not textbook completeness and not full-semester coverage.

The project must be **Sir-notes-scoped, PYQ-shaped, and aggressively filtered**.

## Real scope

The **actual working syllabus for this midsem is Sir's supplied notes**:

- `Sources/Sir_Notes/CV_01.pdf`

Treat that original PDF as the primary authority for what is in scope and for the exact content, diagrams, matrices, formulas, examples and terminology.

The four `CV_01_pages_*.md` files are convenience transcriptions only. They may be used for fast search/navigation, but they are **not the primary source** and must never override the original PDF. If anything is unclear, visual, numerical, missing or inconsistent, verify it in `CV_01.pdf`.

The official syllabus is **reference only**, not the scope boundary. Topics from it that are absent from Sir's notes may be added only as limited supplementary coverage when they are plausible for this paper, especially when supported by PYQs or class guidance.

## Current class guidance

Read `Sources/class_guidance.md` before making priority decisions.

Reported guidance includes:

- scope wording: “Till image processing and video analysis”
- likely 2 numericals
- 3 theoretical questions
- one 2-mark question
- front scatter vs back scatter explicitly mentioned

## Source hierarchy

Use sources with these roles:

1. **Sir's original notes PDF — scope + content authority**
   - `Sources/Sir_Notes/CV_01.pdf`
2. **Current class guidance — priority modifier**
   - `Sources/class_guidance.md`
3. **PYQ Markdown files — primary question-pattern sources**
   - `Sources/PYQs/2025_IT_Computer_Vision_Midsem.md`
   - `Sources/PYQs/Legacy_Fundamentals_of_Image_Processing_A.md`
   - `Sources/PYQs/Legacy_Image_Processing_and_Computer_Vision.md`
   - `Sources/PYQs/Legacy_Fundamentals_of_Image_Processing_B.md`
4. **PYQ PDFs — reference/verification only**
   - open the matching PDF only when the Markdown transcription is unclear, incomplete, visually dependent, or a matrix/figure/mark allocation needs verification.
5. **Official syllabus — supplementary reference only**
   - `Syllabus/syllabus.md`
   - `Syllabus/CV-7th-Semester-IT.pdf`

### Credit-saving rule

Do not repeatedly read expensive source PDFs without reason.

- For PYQs, use the `.md` version first and consult the corresponding PDF only when needed.
- For Sir's notes, the original PDF remains authoritative. Use the helper `.md` transcriptions and `sourcemap.md` for navigation, but verify substantive/visual/numerical content against the PDF when producing final material.
- Reuse completed mappings and analysis rather than re-deriving them in every task.

## Question-scope rule

Use **relevant questions from all supplied PYQs**, including lower-priority legacy papers. A useful question pattern must not be discarded merely because it comes from an older paper.

However, do not import whole old syllabi. Evaluate every PYQ question against the current project scope.

Classify questions as:

- `CORE` — directly supported by Sir's notes. Include and prepare properly.
- `SUPPLEMENTARY` — not directly taught in Sir's notes, but closely related, plausible for this paper, and supported by PYQ/class-guidance/official-syllabus evidence. Cover only to the minimum depth needed to answer the likely exam-style question.
- `EXCLUDE` — old-syllabus, peripheral, or otherwise unlikely to be asked in this paper. Do not put it in the study notes merely because it exists in a PYQ.

When uncertain, prefer **relevance to Sir's notes + question recurrence/style** over age of the paper.

## Inclusion policy

### Include deeply

- everything materially taught in `CV_01.pdf`;
- especially numerical procedures, formulas, worked methods and distinctions present in Sir's notes;
- aligned PYQ question patterns that test those topics.

### Include minimally

A topic outside Sir's notes may be added only when there is a credible exam-safety reason, such as:

- a relevant PYQ asks it and it is a natural extension of material Sir taught;
- class guidance explicitly mentions it;
- the official syllabus contains it and PYQ evidence makes it realistically testable.

Such material must be clearly marked `SUPPLEMENTARY` and kept short.

### Exclude

- official-syllabus leftovers with no realistic current-paper support;
- legacy topics unrelated to Sir's notes;
- textbook expansions that do not improve readiness for the expected paper;
- content added only for completeness.

The objective is **not to miss an important likely question while also not wasting time on material unlikely to appear**.

## Source handling

- Preserve Sir's terminology and framing.
- Preserve original PDF page references in mappings wherever possible.
- Do not infer visual-only content from the helper transcription.
- For numericals, verify formulas, matrices, kernels, graphs and worked values against the original PDF when needed.
- For PYQs, preserve question wording, marks and structure from the `.md` files; verify against PDF only when necessary.
- If sources conflict, record the conflict. Do not silently reconcile it using generic textbook knowledge.
- Keep analysis finite. Do not recursively expand peripheral topics.

## Repository routing

### `sourcemap.md`
Create a compact map of the project:

- Sir-PDF topic -> page range,
- theory / numerical / both,
- relevant PYQ question references,
- class-guidance signal,
- `CORE` / `SUPPLEMENTARY` status where needed.

Sir's original PDF must drive this map. Helper Markdown may accelerate locating content but is not the authority.

### `PYQ_Analysis/question_mapping.md`
Map every potentially relevant question from all four PYQ Markdown files to the current scope. Use `CORE`, `SUPPLEMENTARY`, or `EXCLUDE`, with a short reason. Do not ignore useful questions from legacy papers.

### `PYQ_Analysis/topic_frequency.md`
Measure recurrence only among questions that survive relevance filtering. Keep paper identity visible so an old repeated question does not automatically outweigh current teaching evidence.

### `PYQ_Analysis/gaps.md`
Record only exam-relevant gaps: likely question patterns not properly covered by Sir's notes but worth minimal safety coverage. State exactly why each gap survives filtering and the minimum depth required.

### `Notes/notes.md` — single complete study package
This is the **main and complete study artifact**. It must integrate theory, formulas, diagrams-to-remember, worked numericals and relevant PYQ patterns topic by topic.

Do **not** split theory and numericals into separate study files.

For each topic, use this flow where applicable:

1. explain the concept clearly in connected prose;
2. develop the important definitions, intuition, formulas and distinctions;
3. explain how the method works and when/why it is used;
4. immediately follow with the numerical/worked procedure for that same topic if one is relevant;
5. prefer a relevant PYQ numerical/question as the worked example; otherwise use a worked example from Sir's notes;
6. add concise exam-oriented observations, common mistakes or question variants only when useful.

The writing style should resemble good explanatory university notes: coherent paragraphs, meaningful headings and subheadings, and enough explanation that the user can understand a topic from the notes alone. Avoid one-line pseudo-notes, unexplained keyword dumps, and bullet-only theory. Bullets may be used where they genuinely improve structure, but the core explanation must be prose.

`CORE` topics should be complete enough to learn and answer from. `SUPPLEMENTARY` topics must remain clearly marked and limited to likely exam needs. `EXCLUDE` topics do not enter the notes.

### `Notes/numericals.md`
Do not use this as a separate study artifact. Numerical preparation belongs inside `Notes/notes.md` next to the concept it tests.

### `Notes/revision_notes.md`
Final compact revision layer derived from the completed integrated `Notes/notes.md` and filtered PYQ analysis. It must not introduce new scope.

### `Instructions/`
Follow the task-specific rules in these files together with this `AGENTS.md`.

## Quality rules

- Optimize for marks per study minute.
- Prefer exact formulas, procedures, distinctions, diagrams-to-remember and likely question forms over generic prose.
- Explanations must be clear and substantial enough to learn from; do not reduce important theory to one-liners.
- Keep numerical work immediately adjacent to the theory it depends on.
- Prefer PYQ-based worked examples, then Sir-note examples.
- Do not make notes bloated just to cover the official syllabus.
- Do not omit a relevant PYQ pattern just because its paper is lower priority.
- Do not include material that evidence suggests is unlikely for this midsem.
- Use outside/general knowledge only for minimal supplementary explanation when explicitly needed, and label it as such.

## Current project phase

The source layer is established. The next phase should be **Sir-PDF source mapping + relevance-filtered PYQ analysis**. The integrated final study package in `Notes/notes.md` should be generated only after that mapping is available, unless the user explicitly asks otherwise.