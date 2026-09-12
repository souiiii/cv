# PYQ question mapping

Scope authority is Sir's notes as represented by the completed [sourcemap](../sourcemap.md); page references below are original **CV_01.pdf pages**. Priorities use [class guidance](../Sources/class_guidance.md). The [official syllabus](../Syllabus/syllabus.md) corroborates nearby topics only. No Sir PDF reread or outside research was needed.

**CORE** = directly taught demand; **SUPPLEMENTARY** = a bounded, plausible extension, with minimum coverage specified by `G1`–`G9` in [gaps](gaps.md); **EXCLUDE** = insufficient current-paper support. `T` means explanation/comparison/proof; `N` means an actual calculation, construction or plotted numerical result. A formula in a theory answer does not make it N.

All **41 source question units** are covered (10 IT25, 10 A, 11 IPCV, 10 B). Six units mix taught and additional demands and are split below, giving 47 classified components. Splitting does **not** invent submarks or independent exam questions. Source links retain full wording and data; summaries below preserve the tested demand.

## IT25 — closest historical paper

[2025 IT Computer Vision](../Sources/PYQs/2025_IT_Computer_Vision_Midsem.md): 30 marks, 1.5 hours; answer any three including Q1. Q1 has five 2-mark parts; Q2/Q3 have 5+5; Q4 has 10. `Q1.1`–`Q1.5` follow the Markdown's numbering.

| Question / tested component | Marks | Type | Class | Sir pages and concise reason |
|---|---|---|---|---|
| Q1.1 — digital vs analog image: representation and processing | 2 | T | CORE | 9–12: continuous-to-sampled/quantized representation and digital pixel arrays support the distinction. |
| Q1.2 — binary vs grayscale image and pixel storage | 2 | T | CORE | 11, 47, 53–55: intensity quantization, binary thresholding and 1-bit planes supply the required basics. |
| Q1.3 — intensity range and why L=256 | 2 | T | CORE | 11, 36, 53: bit-depth/level relationship and 8-bit representation; explain that 256 is the 8-bit case, not universal. |
| Q1.4 — raster vs vector structure and scalability | 2 | T | CORE | 7–8: explicit distinction and examples. |
| Q1.5 — lossy vs lossless compression, one example each | 2 | T | SUPPLEMENTARY | G6. p.27 shows compression as a stage, not this distinction; a short same-course PYQ makes minimal coverage worthwhile. |
| Q2(a) — DIP stages and their contribution to quality/information | Shared 5 | T | CORE | 15–28: purpose, stage diagram and application examples are directly taught. |
| Q2(a) — effect of computational cost and input quality | Same 5; no split given | T | SUPPLEMENTARY | G9. Adjacent to pp.15–28, 84–94, but the performance discussion needs a short answer extension. |
| Q2(b) — IR and ultrasound principles; at least two applications each | 5 | T | SUPPLEMENTARY | G7. pp.16–18 give application context, not both modality principles; retain the explicit IT25 demand. |
| Q3(a) — compare negative, log and gamma transforms with effects/examples | 5 | T | CORE | 37–45: formulas, curves, brightness/contrast effects and examples directly match. |
| Q3(b) — filtering and its role/types in noise reduction | Shared 5 | T | CORE | 84–94: spatial filtering, mean/Gaussian kernels and noise context directly support this portion. |
| Q3(b) — filtering vs image warping distinction | Same 5; no split given | T | SUPPLEMENTARY | G8. Filtering is taught, but coordinate warping is not mapped; IT25 and its Q4 justify the small bridge. |
| Q4 — P(2,3): translate (3,−2), rotate 90° CCW, scale (2,1), using homogeneous matrices | 10 | N | SUPPLEMENTARY | G8. No taught geometric-matrix procedure; strong IT25 numerical evidence, corroborated by official Module I transformations. |

## A — legacy Fundamentals of Image Processing

[Paper A](../Sources/PYQs/Legacy_Fundamentals_of_Image_Processing_A.md): 30 marks, 90 minutes; answer any six including Q1, equal marks. Hence **5 per full question** (derived from the instructions); Q1/Q3 subpart allocations are not supplied in Markdown and are not guessed.

| Question / tested component | Marks | Type | Class | Sir pages and concise reason |
|---|---|---|---|---|
| Q1.1 — alpha-trimmed mean filter | Within Q1's 5 | T | SUPPLEMENTARY | G5. Not mapped; a brief definition fits the retained order-statistics/noise-filter extension to pp.84–94. |
| Q1.2 — power-law transformation and applications | Within Q1's 5 | T | CORE | 43–45: explicit power-law and gamma-correction treatment. |
| Q1.3 — construct a 5×5 Gaussian kernel using Pascal's triangle | Within Q1's 5 | N | SUPPLEMENTARY | G1. p.87 teaches a 3×3 Gaussian mask, not this construction; the exact demand also occurs in IPCV and B. |
| Q2 — 4×4, 4-bit input: g=round(10√f), determine output image | 5 | N | CORE | 32–45: pixelwise power-law application; the supplied matrix makes this direct numerical practice. |
| Q3.1 — m-adjacency and advantage, with example | Within Q3's 5 | T | EXCLUDE | No taught adjacency rules; generic neighbourhoods at pp.30–31 do not establish this separate topic. |
| Q3.2 — shortest 4-, 8-, m-paths, V={1,2}, marked p/q | Within Q3's 5 | N | EXCLUDE | Path-length algorithms are absent; legacy repetition does not overcome that scope mismatch. |
| Q4 — first/second derivative sharpening: operators, masks and roles | Shared 5 | T | CORE | 85–87: Prewitt/Sobel, Laplacian and sharpening masks directly anchor this portion. |
| Q4 — fuller derivative explanation, advantages/disadvantages | Same 5; no split given | T | SUPPLEMENTARY | G3. The mapped masks need a concise derivative rationale and comparison to answer the full demand. |
| Q5 — prove that the mean/average filter is low-pass | 5 | T | SUPPLEMENTARY | G4. Mean smoothing is taught at pp.85,87; the proof is not, but is a close, finite extension. |
| Q6 — distance-measure conditions and distances between pixels | 5 | T | EXCLUDE | Metric axioms and pixel-distance families are not taught; no current class/IT25 signal supports them. |
| Q7 — order-statistic filters and applications | 5 | T | SUPPLEMENTARY | G5. Weak/absent in Sir, but repeats IPCV Q3(a) and naturally complements taught noise filtering and IT25 Q3(b). |

## IPCV — legacy Image Processing and Computer Vision

[IPCV paper](../Sources/PYQs/Legacy_Image_Processing_and_Computer_Vision.md): 30 marks, 90 minutes; answer any three including Q1, equal marks. Q1 has five 2-mark parts; Q2–Q4 have 5+5. Q1.1–Q1.5 correspond to printed (a)–(e).

| Question / tested component | Marks | Type | Class | Sir pages and concise reason |
|---|---|---|---|---|
| Q1.1 — image representation through illumination and reflectance | 2 | T | CORE | 10: illumination–reflectance product is explicitly shown in the formation diagram. |
| Q1.2 — categories of images from EM-spectrum energy sources | 2 | T | SUPPLEMENTARY | G7. pp.16–18 give related uses, not a spectrum classification; B Q2 and IT25 modality questions support a compact survey. |
| Q1.3 — construct a 5×5 Gaussian kernel by Pascal's triangle | 2 | N | SUPPLEMENTARY | G1. Same narrow extension of p.87 as A Q1.3 and B Q1.3. |
| Q1.4 — why discrete equalisation generally is not flat, unlike the continuous case | 2 | T | CORE | 70–83, especially 80–83: discrete rounded mapping and non-flat worked result directly support the explanation. |
| Q1.5 — chessboard distance | 2 | T | EXCLUDE | No mapped distance-measure topic; its short length alone is not an inclusion reason. |
| Q2(a) — align two images of one scene to a reference; explain operations | 5 | T | SUPPLEMENTARY | G8. Registration is not taught, but is a bounded companion to IT25 warping/transforms, supported by Module I geometry. |
| Q2(b) — pixel adjacencies and shortest 4-, 8-, m-paths, V={0,1}; explain nonexistent paths | 5 | T+N | EXCLUDE | No taught connectivity/path method; classification does not depend on reconstructing the supplied grid. See transcription correction below. |
| Q3(a) — order-statistics filters with an example | 5 | T | SUPPLEMENTARY | G5. Repeats A Q7 and extends the current noise-filtering material at pp.84–94. |
| Q3(b) — plot histogram and normalized histogram for supplied 0–7 frequencies | Shared 5 | N | CORE | 58–69, 71, 78–79: histogram interpretation, counting and normalization are directly supported. |
| Q3(b) — compute image mean and standard deviation from normalized values | Same 5; no split given | N | SUPPLEMENTARY | G2. These moments are not developed in the mapped histogram section; B Q1.2 independently tests their interpretation. |
| Q4(a) — Laplacian operator and its application | Shared 5 | T | CORE | 85–87: explicit Laplacian and sharpening masks/roles. |
| Q4(a) — restore background features after applying the Laplacian | Same 5; no split given | T | SUPPLEMENTARY | G3. Add the short original-image/Laplacian recombination explanation; this is sharpening, not a demand for general inverse restoration. |
| Q4(b) — homomorphic filtering; control illumination and reflectance | 5 | T | EXCLUDE | p.10's formation model and pp.29,91's frequency-domain mentions do not teach homomorphic filtering; a lone legacy question would add an unsupported method. |

## B — legacy Fundamentals of Image Processing

[Paper B](../Sources/PYQs/Legacy_Fundamentals_of_Image_Processing_B.md): 30 marks, 90 minutes; answer any five including Q1, equal marks. Q1 has three 2-mark parts; other allocations below follow Markdown.

| Question / tested component | Marks | Type | Class | Sir pages and concise reason |
|---|---|---|---|---|
| Q1.1 — prove the 1D DFT matrix is unitary and symmetric | 2 | T | EXCLUDE | Frequency-processing context at pp.29,91 does not teach DFT matrix algebra or this proof. |
| Q1.2 — what histogram standard deviation tells about an image | 2 | T | SUPPLEMENTARY | G2. Brightness/contrast histograms at pp.58–69 supply context; the statistic needs a small extension, reinforced by IPCV Q3(b). |
| Q1.3 — construct a 5×5 Gaussian kernel by Pascal's triangle | 2 | N | SUPPLEMENTARY | G1. Three-paper recurrence of an economical extension to the taught p.87 Gaussian mask. |
| Q2 — types of images formed by EM-spectrum radiation | 6 | T | SUPPLEMENTARY | G7. Repeats IPCV Q1.2 and relates to IT25 Q2(b); retain a short source/principle/application survey, not imaging physics chapters. |
| Q3(a) — g=round(10√f) for the supplied 4×4, 4-bit image | 4 | N | CORE | 32–45: directly executable point/power-law transform; identical formula and input matrix to A Q2. |
| Q3(b) — find the four bit planes of input f(m,n) | 2 | N | CORE | 53–57: direct application of taught bit-plane decomposition; use f, not the transformed g. |
| Q4(a) — m-adjacency and its advantage, with example | 3 | T | EXCLUDE | Absent from taught scope despite repetition in A. |
| Q4(b) — shortest 4-, 8-, m-path lengths, V={1,2} | 3 | N | EXCLUDE | Absent path method; no current evidence warrants importing it. |
| Q5 — first/second derivative sharpening: operators, masks and roles | 3+3 overall | T | CORE | 85–87: first-derivative masks and Laplacian/sharpening kernels are taught. |
| Q5 — explanatory derivative rationale beyond the listed kernels | Same 3+3; no further split | T | SUPPLEMENTARY | G3. A brief finite-difference/edge-response explanation completes the requested theory without a new chapter. |
| Q6 — Hadamard transform; N=8 matrix by equation and Kronecker product | 4+2 overall | T+N | EXCLUDE | No taught transform construction. A Walsh–Hadamard phrase in a cited tracking-paper title is not teaching evidence for this question. |

## Verification and reuse notes

- Only [IPCV PDF, p.1](../Sources/PYQs/Legacy_Image_Processing_and_Computer_Vision.pdf) was opened: Q3(b)'s “histogram is rising” wording was suspicious. The original says **“The histogram of this image is given as:”**; it does not assert monotonic increase. The Markdown frequencies `40,45,55,50,40,35,65,70` for levels `0,…,7` match the PDF. Use the data, not the erroneous “rising” claim.
- The same page shows that IPCV Q2(b) asks **various adjacencies**, not only the Markdown's “determine the 4-adjacency.” The mapping records the broader printed demand; exclusion is unchanged. The source Markdown files were left untouched.
- Other PYQ Markdown is sufficient for classification. Missing grids in excluded adjacency questions need no further PDF work. Unspecified A submarks remain unspecified.
- A Q2 and B Q3(a) repeat the same numerical, so reuse one worked solution later. The stated 4-bit depth describes input f; no output-depth/clipping instruction is given. Do not silently clamp g to the input range. B Q3(b) explicitly decomposes f.
- CORE topics with no supplied PYQ, especially scatter and video analysis, remain in scope. Their priority and the distinction between observed and inferred numerical patterns are recorded in [topic frequency](topic_frequency.md).
