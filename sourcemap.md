# Sir-Notes Source Map

Compact routing index for the midsem; not study notes or a completed PYQ analysis. Page numbers below are **1-based PDF pages** in [CV_01.pdf](Sources/Sir_Notes/CV_01.pdf). The existing page-preserving Markdown files supply the working structure; the original PDF decides content when text is missing or inconsistent. This map reuses the PDF visual checks already completed in this session, including pages omitted by text extraction.

## Sources and reading key

- Working transcriptions: [pp. 1–30](Sources/Sir_Notes/CV_01_pages_001_030.md), [pp. 31–60](Sources/Sir_Notes/CV_01_pages_031_060.md), [pp. 61–90](Sources/Sir_Notes/CV_01_pages_061_090.md), [pp. 91–123](Sources/Sir_Notes/CV_01_pages_091_123.md).
- [Class guidance](Sources/class_guidance.md): “Till image processing and video analysis”; likely **2 numericals, 3 theoretical questions, one 2-mark question**; **front scatter vs back scatter** explicitly mentioned. These are reported signals, not a confirmed mark scheme.
- PYQ shorthand: **IT25** = [2025 IT CV](Sources/PYQs/2025_IT_Computer_Vision_Midsem.md); **A** = [Legacy Fundamentals A](Sources/PYQs/Legacy_Fundamentals_of_Image_Processing_A.md); **IPCV** = [Legacy Image Processing and CV](Sources/PYQs/Legacy_Image_Processing_and_Computer_Vision.md); **B** = [Legacy Fundamentals B](Sources/PYQs/Legacy_Fundamentals_of_Image_Processing_B.md). `Q1.3` means the third listed part of Q1. References are navigation matches, not whole-question classifications. **Partial** identifies a question that asks beyond the mapped slide content.
- **N** in the guidance column = relevant to the reported numerical emphasis, without a topic-specific prediction. **V** = explicit video-analysis scope. **F** = explicit scatter distinction. **—** = no topic-specific class signal; the general theory/short-answer guidance still applies.
- All main-map rows are **CORE**, limited to what the cited slides teach. [Official syllabus](Syllabus/syllabus.md) is reference only; it adds no topics to this map. No supplementary package is approved or developed here.

## Image fundamentals and formation

| Topic / subtopic | PDF pages | Type | Formula, method or visual to locate | Obvious PYQ references | Guidance | Status |
|---|---:|---|---|---|---|---|
| Image; raster vs vector; pixels and digital representation | 6–9, 12 | THEORY | Raster/vector scalability examples; pixel grid; scalar intensity vs colour-vector arrays | IT25 Q1.1, Q1.4 | — | CORE |
| Image acquisition; illumination and reflectance | 10 | THEORY | Optical source → scene → imaging system → image plane; illumination–reflectance product shown in diagram | IPCV Q1.1 | — | CORE |
| Sampling and quantization; intensity levels and storage | 11 | BOTH | Continuous image → spatial sampling → intensity quantization → digital array; bit-depth/level relationship and storage example | IT25 Q1.1, Q1.3 | N | CORE |
| Image formation in scattering media | 13–14 | THEORY | `I_c(x,y) = J_c(x,y)t(x,y) + (1−t(x,y))b_c`; direct, forward-scattered and backscattered light paths; underwater/haze examples | — | **F**: class says “front”; diagram says “forward” | CORE |
| DIP purpose, image processing vs computer vision, applications | 15–18 | THEORY | Improve/transform image vs understand image; medical, remote-sensing, surveillance and other application examples | IT25 Q2(a); Q2(b) applications only, partial | — | CORE |
| Key stages in digital image processing | 19–28 | THEORY | Stage diagram and examples: acquisition, enhancement, restoration, morphology, segmentation, recognition, representation/description, compression, colour processing | IT25 Q2(a); Q1.5 partial (compression stage only) | — | CORE |

## Enhancement and numerical methods

| Topic / subtopic | PDF pages | Type | Formula, method or visual to locate | Obvious PYQ references | Guidance | Status |
|---|---:|---|---|---|---|---|---|
| Enhancement; spatial domain; neighbourhood vs point processing | 29–36 | BOTH | `g(x,y)=T[f(x,y)]`; 1×1 case `s=T(r)`; neighbourhood diagram p.31; point-processing overview p.33; LUT p.36 | IT25 Q3(a), Q3(b) filtering portion; A Q2; B Q3(a) | N | CORE |
| Negative, log/inverse-log and power-law transformations | 37–45 | BOTH | Curve comparison p.37; negative `s=L−1−r` p.38; log `s=c log(1+r)` p.41; power law `s=cr^γ` p.43; gamma-correction visual p.44 | IT25 Q3(a); A Q1.2, Q2; B Q3(a) | **N** | CORE |
| Contrast stretching and thresholding | 32–34, 46–49 | BOTH | Piecewise curve through `(r1,s1)`, `(r2,s2)`; identity and threshold limiting cases; before/after images | IT25 Q1.2 partial (binary-image link) | N | CORE |
| Gray-level slicing | 50–52 | BOTH | Selected intensity interval: suppress background vs preserve background; paired transformation graphs | — | N | CORE |
| Bit-plane slicing | 53–57 | BOTH | Eight 1-bit planes; LSB/MSB; plane 7 and threshold 128; plane-stack and separated-image visuals | B Q3(b); IT25 Q1.2–Q1.3 supporting basics | **N** | CORE |
| Histograms and brightness/contrast interpretation | 58–69 | BOTH | Frequency vs gray level; dark, bright, low-contrast and high-contrast examples; comparison p.69; normalization used at pp.71,79 | IPCV Q3(b) histogram/normalization; B Q1.2 partial (standard deviation not developed here) | N | CORE |
| Histogram equalisation: CDF, mapping and discrete result | 70–83 | BOTH | CDF formula p.71; transformation curves pp.72–76; step overview p.77; complete **4×4, L=8 worked example pp.78–83**; `s_k=round[(L−1)CDF(r_k)]` p.80 | IPCV Q1.4; Q3(b) supplies related histogram practice, not an equalisation question | **N** | CORE |
| Spatial filtering / convolution and padding | 84–86 | BOTH | Flip kernel in both directions → centre → multiply → sum; preserve output size by padding p.84; overview p.85; **3×3 image/kernel/output and boundary placements p.86** | IT25 Q3(b) filtering/noise-reduction portion | **N** | CORE |
| Mean and Gaussian smoothing kernels | 85, 87 | BOTH | p.87: mean `1/9 × [[1,1,1],[1,1,1],[1,1,1]]`; Gaussian `1/16 × [[1,2,1],[2,4,2],[1,2,1]]`; smoothing role p.85 | A Q1.3, Q5; IPCV Q1.3; B Q1.3 — partial: Pascal construction/low-pass proof exceed the displayed kernels | **N** | CORE |
| First/second derivative kernels: Prewitt, Sobel, Laplacian | 85–87 | BOTH | Paired directional Prewitt/Sobel masks p.87; Laplacian `[[0,1,0],[1,−4,1],[0,1,0]]`; edge/sharpening roles p.85 | A Q4; B Q5; IPCV Q4(a) — partial: fuller comparisons/background recombination require later gap review | N | CORE |
| Restoration vs enhancement; degradation model | 88–91 | THEORY | Known/estimated degradation vs visual improvement; degradation–noise–restoration block diagram; `g=h*f+η` p.89; noise-only and frequency-processing routes pp.90–91 | IT25 Q2(a), Q3(b) partial | — | CORE |
| Noise models and image/histogram appearance | 92–94 | THEORY | Gaussian, Rayleigh, Gamma, exponential, uniform, impulse/salt-and-pepper; source associations, PDF curves, estimating parameters from a flat region | IT25 Q3(b) noise context, partial | — | CORE |

## Video analysis and taught model overviews

| Topic / subtopic | PDF pages | Type | Formula, method or visual to locate | Obvious PYQ references | Guidance | Status |
|---|---:|---|---|---|---|---|---|
| Digital video and spatiotemporal representation | 95–97 | BOTH | Sequence of 2D frames as a 3D `(x,y,t)` signal; frame stack and resolution/frame-count example p.97 | — | V; small calculation possible | CORE |
| Video-processing stages, operations and applications | 98–99 | THEORY | Acquisition → sampling → quantization → compression → storage/transmission → playback; spatial/temporal processing, motion analysis, enhancement, segmentation | — | V | CORE |
| Video processing vs video analytics; surveillance pipeline | 100–102 | THEORY | Comparison table p.100; detection + tracking p.101; capture → preprocessing/features → spatiotemporal modelling → anomaly/intrusion → alerts/response p.102 | — | **V** | CORE |
| Object detection by background modelling vs object modelling | 103–104 | BOTH | Background update, subtraction, thresholding and postprocessing p.103; target model/features, search, matching and localization p.104 | — | V; p.103 arithmetic is a possible variant | CORE |
| Frame differencing and moving-object detection | 105–108 | BOTH | `D_t=abs(I_t−I_(t−1))`; binary threshold `D_t≥T` p.106; postprocessing, flow diagram, limitations and applications | — | **V + N**; no supplied matching PYQ | CORE |
| Intruder detection: multi-frame differencing | 109–110 | BOTH | Two-/three-frame comparison visual p.109; five-frame algorithm and Boolean/difference flow p.110. Retain the displayed procedure; no paper-level expansion | — | V | CORE |
| Gaussian Mixture Model background subtraction | 111 | THEORY | Multiple adaptive Gaussian backgrounds per pixel; non-static background/illumination motivation; foreground when distributions do not fit | — | V | CORE |
| Wronskian Change Detection Model | 112 | BOTH | Region-of-support vector, spatio-contextual diagram and displayed change measure; return to this page for exact equation if used numerically | — | V; formula shown, no worked numerical | CORE |
| Intruder detection/tracking in crowd; particle filter framework | 113–114 | THEORY | GMM clustering/reassignment diagram p.113; tracking state `{xc,yc,vx,vy,ax,ay}` and particles/windows at `t−1`, `t` p.114 | — | V | CORE |
| Deep-learning detection architecture and named AI models | 115–118 | THEORY | Backbone → neck → detection head; class/box/objectness outputs; processing/NMS p.117; FPN/PAN/BiFPN roles p.118; model-to-task list p.116 | — | V; slide-level coverage | CORE |
| Working of a CNN model | 119–121 | BOTH | Convolution → ReLU → max pooling → flatten → fully connected → softmax; toy matrix/feature-map illustrations. Repeated workflow panels, not three separate topics | — | V; illustrative arithmetic only | CORE |

## Priority and reuse cautions

- **First numerical routes:** point/power-law transforms (pp.33–45; IT25/A/B links), histogram equalisation (pp.78–83), spatial convolution and kernels (pp.84–87). Bit planes (pp.53–57; B Q3(b)) are another direct match. Frame differencing (pp.105–108) is a source-supported video variant, not a recurring PYQ claim.
- **First theory routes:** explicit scatter distinction (p.13), DIP stages (pp.19–28), intensity-transform comparisons (pp.37–45), restoration/noise (pp.88–94), and video-processing/analytics plus detection pipelines (pp.96–108). This is preparation ordering from teaching, obvious PYQ matches and guidance, not a frequency analysis.
- **Recovered visual content:** p.11 contains sampling/quantization; p.13 contains scatter paths; p.15 adds DIP vs CV; pp.33,77,85 contain method overviews; p.86 contains a convolution numerical; pp.97–99,102–108 contain video workflows/formulas; p.110 contains an algorithm beyond the helper's citation; p.112 contains an equation; pp.115,117,119–121 contain architecture/CNN diagrams. These pages are not blank simply because the helpers omit their text.
- **Numerical conventions:** p.71 shows a normalized CDF, whereas p.80 gives the rounded integer-level mapping; preserve that distinction and inspect p.71's summation indexing if reproducing it. The helper p.39 uses `L−f`, while verified p.38 explicitly uses `L−1−r` for levels `[0,L−1]`; do not silently carry the helper notation into a numerical. For convolution use the p.84 flip/padding convention and p.86 placements, not a guessed correlation convention.
- **Limits of PYQ links:** the map does not establish that whole questions are covered. Pascal's 5×5 construction, histogram mean/standard deviation, lossy/lossless distinctions, imaging-modality principles, warping/geometric matrices and fuller derivative-filter answers need the later relevance/gap decision. They are not added as taught topics here. No PYQ PDFs were needed for these navigation links.
- **Scope boundaries:** morphology/compression/colour and named AI systems receive the depth actually shown, not full algorithms or model courses. The CNN slides remain CORE despite the official-reference warning about Module III, because Sir's PDF explicitly includes them. No external papers cited on the slides were opened. Pages 1–5 are title/motivational visuals; pp.122–123 are references/closing, with no additional study topic.
