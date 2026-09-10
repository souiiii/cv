# CV Mid-Semester Project Instructions

## Purpose

This repository is for **Computer Vision mid-semester preparation**. The goal is to produce compact, exam-ready material from the current teaching sources, with strong numerical coverage and only limited gap-filling from old papers.

Do not turn this into a full-semester Computer Vision project unless explicitly asked.

## Current exam context

- Current target: **7th-semester IT Computer Vision midsem**.
- The official syllabus PDF is for the **full semester**.
- For current preparation, treat **Module I as the formal syllabus boundary**. Later Module II/III material belongs to endsem unless current class guidance explicitly says otherwise.
- Reported class guidance:
  - “Till image processing and video analysis”
  - likely 2 numericals
  - 3 theoretical questions
  - one 2-mark question
  - front scatter vs back scatter explicitly mentioned

Read `Sources/class_guidance.md` before making scope or priority decisions.

## Source priority

Use sources in this order:

1. **Sir's supplied notes** — primary authority for what to study deeply.
   - `Sources/Sir_Notes/CV_01_pages_001_030.md`
   - `Sources/Sir_Notes/CV_01_pages_031_060.md`
   - `Sources/Sir_Notes/CV_01_pages_061_090.md`
   - `Sources/Sir_Notes/CV_01_pages_091_123.md`
   - These are page-preserving machine-readable transcriptions of the supplied `CV_01.pdf` titled *Image Processing and Video Analysis*.
2. **Current class guidance** — `Sources/class_guidance.md`.
3. **Official syllabus** — `Syllabus/syllabus.md` and `Syllabus/CV-7th-Semester-IT.pdf`.
4. **Closest historical PYQ** — `Sources/PYQs/2025_IT_Computer_Vision_Midsem.md`.
5. **Older partially aligned image-processing PYQs** — secondary evidence only:
   - `Sources/PYQs/Legacy_Fundamentals_of_Image_Processing_A.md`
   - `Sources/PYQs/Legacy_Image_Processing_and_Computer_Vision.md`
   - `Sources/PYQs/Legacy_Fundamentals_of_Image_Processing_B.md`

## Core interpretation rule

**Sir's notes dominate preparation priority.**

Do not infer the current midsem scope from old papers. A topic appearing repeatedly in legacy papers is not enough to promote it into the main notes.

If a topic is:

- in Sir's notes -> learn it properly and preserve Sir's terminology;
- in Sir's notes and numerical -> give it strong worked-practice coverage;
- in the official midsem syllabus / relevant PYQ but absent from Sir's notes -> classify it as a `gap/secondary` topic and cover only enough to solve or answer the standard exam-style question, unless current class evidence elevates it;
- only in an old mismatched paper -> do not add it to the main preparation material by default.

The project should therefore be **Sir-notes-first, PYQ-informed, syllabus-bounded**.

## Source handling rules

- Preserve original page numbers when mapping Sir's notes.
- The Sir-note files are machine transcriptions. Some visual-only pages, diagrams, matrices or formatting may not be captured perfectly.
- Do **not hallucinate missing visual content**. If a transcript says a page is visual/blank or a matrix is ambiguous, mark the uncertainty instead of inventing details.
- Reuse the existing source files; do not repeatedly re-derive the same material.
- Keep analysis finite and task-oriented. Do not recursively expand topics or over-analyse peripheral material.

## Repository routing

### `sourcemap.md`
Use this for the map of the current material:

- topic -> Sir-note page range,
- whether theory/numerical/both,
- official Module-I mapping where relevant,
- PYQ evidence references,
- confidence / gap status.

Do not make it a second set of notes.

### `PYQ_Analysis/question_mapping.md`
Map relevant PYQ questions to Sir-note topics/page ranges. Clearly distinguish:

- `CURRENT-ALIGNED` — supported by Sir's notes,
- `RELATED-GAP` — officially related but absent/weak in Sir's notes,
- `LEGACY-ONLY` — should not drive current preparation.

### `PYQ_Analysis/topic_frequency.md`
Count recurrence only after filtering for syllabus/current-source alignment. Do not mix unrelated older-syllabus questions into the frequency signal.

### `PYQ_Analysis/gaps.md`
Record only genuine gaps between:

- Sir's notes,
- current Module-I boundary,
- closest/current-aligned PYQ patterns,
- explicit class guidance.

For each gap, state the minimum depth needed for exam safety. Do not automatically recommend full-topic study.

### `Notes/notes.md`
Main exam-ready theory notes. Generate only when the user explicitly asks for note generation or when `Instructions/how_to_notes.md` has been populated and the task says to proceed.

### `Notes/numericals.md`
Worked numerical methods and practice patterns. Prioritize numerical material actually present in Sir's notes, especially transformations, histogram/equalization, filtering/kernels and any other directly supported numerical procedures.

### `Notes/revision_notes.md`
Very compact final revision material derived from the completed main notes and numericals; do not create it prematurely.

### `Instructions/`
These files define how later note, numerical, PYQ and revision generation should behave. If they are empty, do not invent a large workflow without being asked. Follow the user's current prompt and this `AGENTS.md`.

## Quality rules

- Optimize for a 30-mark midsem, not textbook completeness.
- Prefer exact formulas, procedures, distinctions and worked patterns over generic prose.
- Separate **source-derived content** from any minimal gap explanation added from general knowledge.
- Never silently replace Sir's framing with a standard textbook treatment.
- Avoid bloated notes and duplicated explanations.
- For PYQs, preserve marks and question structure where available.
- If evidence conflicts, explicitly flag it rather than forcing a false reconciliation.

## Current project phase

The source layer is now established. The next sensible phase is **source mapping + filtered PYQ analysis** before designing/generating the final notes.

Do not generate all final notes in the same pass unless the user explicitly asks for that.
