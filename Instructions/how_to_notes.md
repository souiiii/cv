# How to Write the Complete Study Notes

Use `Sources/Sir_Notes/CV_01.pdf` as the content authority and `sourcemap.md` + filtered PYQ analysis as the routing layer.

`Notes/notes.md` is the **single complete study package**. It must combine explanation, formulas, diagrams-to-remember, worked numericals and relevant PYQ patterns in one coherent topic-by-topic document.

Do not write terse revision-style notes here. The user should be able to learn a topic properly from this file alone.

## Writing style

Write in clear explanatory prose similar to good university notes:

- use meaningful `#`, `##`, `###` headings;
- explain concepts in connected paragraphs, not keyword fragments;
- avoid one-line definitions unless the idea is genuinely trivial;
- explain what a concept means, why it matters, how it works, and how it is used in an exam-relevant context;
- use bullets only when they improve structure, such as listing cases, properties, steps or comparisons;
- introduce symbols before using them;
- place equations immediately after the explanation that motivates them;
- explain the meaning of important equations rather than dumping formulas.

The tone should be concise but pedagogical: enough prose to understand and remember the concept, without textbook-level padding.

## Topic flow

For every `CORE` topic, follow this order where applicable:

1. **Concept and intuition** — explain the topic in prose.
2. **Important definitions / distinctions** — only what is realistically useful for the paper.
3. **Formula or method** — state it clearly and explain the terms.
4. **How to apply it** — describe the reasoning/procedure.
5. **Worked numerical or question** — immediately after the theory when the topic has a numerical component.
6. **Exam relevance** — short note on likely question forms, common mistakes, or distinctions if useful.

Do not place all numericals in a distant chapter. A student should be able to finish one topic completely before moving to the next.

## Numericals inside the notes

Numerical preparation belongs inside `Notes/notes.md`.

For each numerical topic:

- prefer an aligned **PYQ numerical** as the worked example;
- if no suitable PYQ exists, use a numerical/example from Sir's notes;
- if neither provides a clean worked problem but the method is clearly examinable, create only the minimum representative practice example needed;
- show the solution step by step;
- state formulas before substitution;
- show intermediate values where they matter;
- explain non-obvious choices, indexing, normalization, rounding, kernel placement or matrix order;
- include common calculation mistakes only when they are realistic exam traps.

If the numerical comes from a PYQ, identify the source/question succinctly. Do not unnecessarily reproduce the entire paper around it.

## PYQ integration

Use filtered PYQ analysis to shape both depth and examples.

- A repeated relevant theory question should cause that concept to be explained sufficiently to write a proper answer.
- A repeated numerical form should receive a complete worked pattern.
- Useful questions from legacy papers may be used if they survived the current-scope relevance filter.
- Do not insert `EXCLUDE` questions or old-syllabus material simply for completeness.

## Scope handling

For `CORE` topics:

- preserve Sir's terminology and framing;
- cover them sufficiently to understand and answer likely questions;
- verify visual/formula-heavy details in the original PDF when needed.

For `SUPPLEMENTARY` topics:

- clearly mark them as supplementary;
- explain only the amount needed for the realistic question pattern that justified inclusion;
- do not turn them into full textbook chapters.

Do not include `EXCLUDE` topics.

## Final quality bar

`Notes/notes.md` should function as a **learn + practice + exam-prep document**, not merely a theory summary.

After completing a topic from the notes, the user should normally be able to:

- explain the concept in an exam answer;
- recall and interpret the important formula(s);
- solve the standard numerical form if applicable;
- recognize relevant PYQ variants;
- avoid the common mistakes worth caring about.

Avoid duplicated explanations, filler, generic conclusions and excessive prose.