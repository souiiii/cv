# Relevance-filtered PYQ recurrence and priorities

Use with [question mapping](question_mapping.md) and [sourcemap](../sourcemap.md). **Paper recurrence** means the number of distinct supplied papers testing a retained pattern, at most one occurrence per paper in each row. Cells preserve question identity; question-component counts are secondary and are not mark totals. IT25 is the closest course/branch paper; A, IPCV and B are legacy ETC papers.

CORE and SUPPLEMENTARY counts are separate. A mixed question contributes only its explicitly classified portion to each table; the two tables must not be added into an “importance score.” Excluded questions contribute nothing. Related demands grouped in one family are identified below rather than claimed to be identical repeats.

## CORE recurrence

`T` = theory; `N` = requested numerical procedure. These describe the **PYQ demand**, not every possible way to test the topic.

| Retained pattern | IT25 | A | IPCV | B | Papers | Components / type |
|---|---|---|---|---|---:|---|
| Image representation, binary/grayscale, bit depth, raster/vector | Q1.1–Q1.4 | — | — | — | 1 | 4 / T |
| DIP stages and purpose | Q2(a), stages | — | — | — | 1 | 1 / T |
| Intensity transforms / power law | Q3(a), T | Q1.2, T; Q2, N | — | Q3(a), N | **3** | 4 / T+N |
| Illumination–reflectance representation | — | — | Q1.1 | — | 1 | 1 / T |
| Histogram plotting and normalization | — | — | Q3(b), plotting | — | 1 | 1 / N |
| Discrete equalisation and non-flat output | — | — | Q1.4 | — | 1 | 1 / T |
| Spatial filtering and noise reduction | Q3(b), filtering | — | — | — | 1 | 1 / T |
| Derivative/sharpening operators, masks and roles | — | Q4, core portion | Q4(a), operator portion | Q5, core portion | **3** | 3 / T |
| Bit-plane decomposition | — | — | — | Q3(b) | 1 | 1 / N |

The intensity-transform family spans three papers, but the **calculated square-root transform occurs in two**, A Q2 and B Q3(a), with identical input and formula: two paper appearances, **one distinct numerical template**. IT25 Q3(a) asks a comparison with examples, not a matrix calculation. Derivative questions are theory demands despite involving masks.

## SUPPLEMENTARY recurrence

These counts retain only the finite extensions approved in [gaps](gaps.md). A three-paper legacy repeat remains supplementary when Sir taught only its prerequisite.

| Gap / retained pattern | IT25 | A | IPCV | B | Papers | Components / type |
|---|---|---|---|---|---:|---|
| G1 — 5×5 Gaussian by Pascal construction | — | Q1.3 | Q1.3 | Q1.3 | **3** | 3 / N; same construction |
| G2 — histogram mean/standard deviation | — | — | Q3(b), moments, N | Q1.2, interpretation, T | **2** | 2 / T+N; related demands |
| G3 — derivative rationale/comparison and Laplacian recombination | — | Q4, extension | Q4(a), background portion | Q5, extension | **3** | 3 / T; shared family, not identical questions |
| G4 — mean-filter low-pass proof | — | Q5 | — | — | 1 | 1 / T |
| G5 — order-statistics filters, including alpha-trimmed mean | — | Q1.1; Q7 | Q3(a) | — | **2** | 3 / T; general survey repeats twice, alpha-trimmed specifically once |
| G6 — lossy vs lossless compression | Q1.5 | — | — | — | 1 | 1 / T |
| G7 — imaging sources/modalities | Q2(b), IR/ultrasound | — | Q1.2, EM categories | Q2, EM categories | **3** | 3 / T; EM survey repeats twice, IR/ultrasound specifically once |
| G8 — geometric transformation / warping / registration | Q3(b), warping, T; Q4, N | — | Q2(a), registration, T | — | **2** | 3 / T+N; one matrix numerical, not two |
| G9 — computational cost/input-quality effects | Q2(a), performance | — | — | — | 1 | 1 / T |

Audit: **17 CORE + 20 SUPPLEMENTARY + 10 EXCLUDE components = 47**, representing 41 source question units after six mixed units were split. Counts show coverage, not predicted question probabilities; papers with more subparts naturally supply more components.

## Exam-focused ordering

| Priority | Numerical preparation | Theory / short-answer preparation | Evidence and practical limit |
|---|---|---|---|
| **First: directly taught** | Pixelwise intensity/power-law calculation; histogram equalisation procedure; spatial convolution with kernel flip/padding; bit planes | Intensity-transform comparisons; DIP stages; digital-image distinctions; derivative masks/roles; restoration vs enhancement and noise models | Direct Sir coverage plus IT25 and relevant legacy matches. Equalisation's complete numerical is Sir pp.78–83; convolution's is p.86. Neither has an exact supplied calculation PYQ. |
| **Explicit class emphasis** | Simple frame-difference/threshold application as a video variant, after demonstrated image-processing numericals | **Front/forward scatter vs backscatter**, p.13; video representation, processing vs analytics, detection/tracking pipelines, pp.95–114 | Scatter is explicitly named; scope explicitly reaches video analysis. Both have **zero supplied PYQ occurrences**, which does not lower them out of scope. Frame arithmetic is a plausible variant, not a guaranteed numerical. |
| **First supplementary safety work** | G1 Pascal Gaussian; G2 histogram moments; G8 the single IT25 homogeneous-transform sequence | G3 derivative answer completion; G6 compression distinction; G7 IR/ultrasound answer and short EM survey; G8 filtering vs warping | Small extensions with recurrence, or explicit IT25 evidence. The historical 10 marks on IT25 Q4 justify one matrix example, not a geometry course. |
| **Finish bounded extensions** | No extra numerical bank required | G4 short low-pass proof; G5 compact order-statistics survey/example; G9 one performance paragraph | Close to taught filtering/stages; keep to the gap limits. |

The reported pattern is likely **2 numericals, 3 theoretical questions and one 2-mark question**; it is not a verified current mark scheme or an instruction to reproduce IT25's Q1 structure. Prepare both substantive answers and short distinctions.

**Remain CORE without recurrence:** contrast stretching/thresholding, gray-level slicing, sampling/quantization, restoration/noise, and the video/model topics indexed by Sir. Wronskian, particle-filter state and CNN illustrations do not become numerical priorities merely because formulas or matrices appear. Keep those at the mapped explanatory depth. Do not let legacy counts displace current teaching or the explicit scatter/video signals.
