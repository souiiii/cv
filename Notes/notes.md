# Computer Vision Midsem — Complete Study Notes

These notes cover Sir's **Image Processing and Video Analysis** material, with theory and calculations together. Unmarked sections are **CORE**. Sections explicitly labelled **SUPPLEMENTARY G1–G9** contain only the approved exam-safety additions. Page references are original pages of [CV_01.pdf](../Sources/Sir_Notes/CV_01.pdf).

Scope and priorities follow the [sourcemap](../sourcemap.md), [question mapping](../PYQ_Analysis/question_mapping.md), [filtered recurrence](../PYQ_Analysis/topic_frequency.md), [bounded gaps](../PYQ_Analysis/gaps.md), and [class guidance](../Sources/class_guidance.md). The reported paper has likely two numericals, three theory questions and one 2-mark question; this is guidance, not a confirmed mark scheme. **Front/forward scatter vs backscatter is explicitly highlighted.** Video topics remain important even without a matching PYQ.

PYQ abbreviations: **IT25** = [2025 IT CV](../Sources/PYQs/2025_IT_Computer_Vision_Midsem.md), **A** = [Legacy Fundamentals A](../Sources/PYQs/Legacy_Fundamentals_of_Image_Processing_A.md), **IPCV** = [Legacy Image Processing and CV](../Sources/PYQs/Legacy_Image_Processing_and_Computer_Vision.md), **B** = [Legacy Fundamentals B](../Sources/PYQs/Legacy_Fundamentals_of_Image_Processing_B.md).

For numerical readiness, give early attention to intensity transforms, histogram equalisation, convolution/padding and bit planes, followed by the supplementary Pascal kernel, histogram moments and IT25 geometric-transform example. Learn the surrounding explanations as well: several PYQs ask theory about these same methods.

## 1. Images, digital representation, sampling and quantization

*Sir pp.6–12; IT25 Q1.1–Q1.4.*

An **image** is a visual representation of an object, scene or information. In image processing, a grayscale image is represented by an intensity function: its coordinates identify a location, and its value describes brightness there. A **digital image** stores a finite array of picture elements, or **pixels**, at discrete locations. A grayscale pixel contains one intensity value; a colour pixel can contain a vector of channel values. Thus an image array contains measured information, not merely a collection of visible squares.

An **analog image representation** varies continuously in position and intensity. A digital representation samples positions and quantizes intensities into discrete values that a computer can store and manipulate numerically. The distinction concerns representation: displaying a digital image smoothly does not make its stored data continuous.

### 1.1 Raster, vector, binary and grayscale

These distinctions answer different questions. Raster/vector describes how image content is represented; binary/grayscale describes the intensity information stored in pixels.

| Representation | Structure and consequence |
|---|---|
| **Raster** | A pixel grid, suitable for photographs. Enlargement reveals or interpolates a finite set of samples, so detail cannot increase merely by scaling. |
| **Vector** | Mathematical shapes, lines and curves. Shapes can be redrawn at a new size without the pixelation of an enlarged fixed raster; logos are a common example. |
| **Binary image** | Two possible pixel values, logically 0 and 1, requiring one bit per pixel in an ideal packed representation. A displayed white pixel may be shown as 255 while still representing logical 1. |
| **Grayscale image** | Multiple brightness levels without separate colour channels. With b bits per pixel there are L=2^b possible levels, conventionally numbered 0 to L−1. |

For an 8-bit grayscale image, **L=256**, with values **0–255**. There are 256 levels, not a maximum value of 256. This is an 8-bit convention, not a rule that all grayscale images must have 256 levels.

### 1.2 Sampling and quantization

**Sampling** selects discrete spatial positions. If the spacing between positions is Δx horizontally and Δy vertically, the samples of continuous image f are

\[
f[m,n]=f(m\Delta x,n\Delta y).
\]

**Quantization** maps each sampled intensity to one of the allowed levels. Writing Q for this mapping, the stored image is

\[
g[m,n]=Q\{f(m\Delta x,n\Delta y)\}.
\]

Smaller sampling intervals provide more spatial samples and finer spatial resolution. More quantization levels provide finer intensity resolution. Increasing one does not automatically increase the other: a large image may still have only two intensity levels.

**Diagram to remember — p.11:** continuous image → spatial sampling/grid → intensity quantization/staircase → digital array. Label the spatial spacing separately from the intensity levels.

**Worked storage example — Sir p.11.** A 512×512 grayscale image at 8 bits/pixel has

\[
N=512\times512=262144\text{ pixels},\qquad
\text{storage}=N\times8=2097152\text{ bits}.
\]

Divide by 8 to obtain **262144 bytes = 256 KiB**, ignoring headers/compression. Sir labels this approximately 256 KB. The calculation uses a single grayscale value per pixel; do not add three colour channels unless the question specifies them.

## 2. Image formation and scattering

*Sir pp.10,13–14; IPCV Q1.1; explicit class scatter guidance.*

### 2.1 Illumination and reflectance

An imaging system receives light from a scene and forms an image on its image plane. In Sir's basic formation diagram, the image intensity depends on both the light incident on the scene and the fraction reflected toward the imaging system:

\[
f(x,y)=i(x,y)r(x,y),
\]

where i is **illumination** and r is **reflectance**. A dark pixel may therefore result from weak illumination, low reflectance, or both. This product explains why a pixel value is not simply an intrinsic property of the object.

**Diagram to remember — p.10:** optical source → physical scene → imaging system → image plane/pixel grid. Put the illumination–reflectance product between scene and recorded image.

### 2.2 Front/forward scatter vs backscatter

In underwater or hazy scenes, light interacts with suspended particles before reaching the camera. Sir distinguishes three paths. **Direct light** travels from the object to the camera and carries scene detail. **Forward-scattered light** starts from the object but is deflected by particles on its way to the camera; spreading light from an object point blurs its appearance. **Backscattered light** is illumination scattered by particles toward the camera without first conveying the object's reflected appearance; it adds a veil that reduces contrast.

| Feature | Front/forward scatter | Backscatter |
|---|---|---|
| Relevant path in Sir's diagram | Object → particle → camera | Illumination → particle → camera |
| Main image effect | Spreading of object light; blur and loss of fine detail | Added background/veiling light; reduced object–background contrast |
| What to label | Deflected object-light path | Particle-light path entering the camera |

The reported class wording is **“front scatter”**; the p.13 diagram labels **“forward scattered light.”** Use that connection explicitly when answering.

```text
Illumination ──> object ─────────────────────> camera   (direct)
                   └──> particle ──────────> camera   (forward scatter)
Illumination ──────────> particle ──────────> camera   (backscatter)
```

Sir's simplified image-formation model is

\[
I_c(x,y)=J_c(x,y)t(x,y)+[1-t(x,y)]b_c.
\]

Here I_c is the **acquired image**, J_c the **clear image**, t the **transmission map**, and b_c the **surrounding light**, with c denoting a colour channel. The first term is transmitted scene information; the second is the surrounding-light contribution. When t is close to 1, the acquired value is close to the clear value. When t is small, the surrounding-light term dominates. The diagram explains forward scatter, but this displayed equation does not contain a separate forward-blur kernel; do not invent one in the answer.

### 2.3 SUPPLEMENTARY G7 — imaging modalities and EM sources

*IT25 Q2(b), IPCV Q1.2, B Q2.*

Images can be formed from different physical signals. For an EM-spectrum question, identify the radiation, what the detector measures, and a representative use; wavelengths and detailed device physics are unnecessary here.

| EM band | Formation principle and representative use |
|---|---|
| Gamma rays | Detect high-energy radiation, for example emissions associated with a tracer, to map its distribution in nuclear imaging. |
| X-rays | Measure radiation transmitted through an object; differing attenuation produces contrast, as in bone or baggage imaging. |
| Ultraviolet | Record UV interaction or UV-induced fluorescence, useful for inspecting surface features or fluorescent specimens. |
| Visible light | Record reflected/transmitted visible illumination; ordinary cameras and machine inspection. |
| Infrared | Record reflected IR or emitted thermal IR, depending on the band/system; thermal inspection and night observation. |
| Microwaves | Record emitted radiation or transmitted-signal echoes, as in radar imaging for terrain or weather observation. |
| Radio waves | Detect radio-frequency signals; MRI uses RF excitation and measured responses in a magnetic field to form images. |

**Infrared imaging** uses an IR-sensitive detector to convert incoming infrared radiation into an image. Thermal IR systems represent differences in emitted radiation associated with temperature, allowing observation when visible illumination is poor. Two suitable applications are **night surveillance** and **detecting overheating electrical equipment**. Not all IR images are thermal: some use reflected IR illumination.

**Ultrasound imaging** uses a transducer to send high-frequency sound pulses into a medium and receive echoes from interfaces. Echo travel time indicates depth and echo strength contributes image brightness; repeated measurements build a cross-sectional image. Two applications are **prenatal imaging** and **industrial internal-defect inspection**. Ultrasound is **sound, not electromagnetic radiation**, so do not place it inside the EM-band table.

## 3. Digital image processing: purpose and stages

*Sir pp.15–28; IT25 Q2(a).*

**Digital image processing (DIP)** is the computer-based representation and manipulation of pictorial information. It may improve an image for human interpretation or prepare information for machine processing, storage and transmission. Sir's distinction is useful: image processing **improves/transforms the image**, while computer vision **understands the image**. Removing noise from an X-ray is image processing; identifying an abnormality in it is image analysis/computer vision.

The stages below describe the functions in Sir's diagram. They are not a requirement that every application execute every stage in a rigid sequence. For example, enhancement may help segmentation, while compression supports storage at a different point in a system.

| Stage | Meaning and contribution |
|---|---|
| **Image acquisition** | Obtain the image with a sensor and convert it into usable digital samples. Poor acquisition limits the information available later. |
| **Image enhancement** | Make relevant information easier to see or use, such as by improving contrast. Suitability depends on the application. |
| **Image restoration** | Estimate the original image from a degraded observation using a known or estimated degradation model. |
| **Morphological processing** | Process image shapes/structures, for example cleaning small unwanted features in a mask. Sir introduces its role here rather than a full morphology course. |
| **Segmentation** | Separate an image into meaningful regions or objects so subsequent analysis can focus on them. |
| **Object recognition** | Assign meaning or an identity/class to an object, rather than merely marking a region. |
| **Representation and description** | Represent regions or boundaries and describe them through useful properties/features for later interpretation. |
| **Image compression** | Reduce the data needed to store or transmit the image. |
| **Colour image processing** | Use and manipulate colour information when it is relevant to the task. |

**Diagram to remember — pp.19–28:** draw acquisition, enhancement, restoration, morphological processing, segmentation, recognition, and representation/description as the main blocks; include compression and colour processing as supporting blocks. Explain each block's contribution rather than listing names alone.

Sir's applications include medical and biological imaging; remote sensing/GIS and meteorology; robotics and autonomous vision; surveillance, biometrics and forensics; industrial/agricultural quality inspection; entertainment; document/handwriting analysis; and cultural-heritage restoration. In an exam, connect a few examples to a function: segmentation isolates a region, enhancement exposes faint information, and recognition supplies an object label.

### 3.1 SUPPLEMENTARY G9 — cost and input quality

Processing cost grows with the amount of image data and the work performed at each location. For example, increasing image resolution or the size of a sliding filter means more pixel operations. Input noise, blur or poor contrast can hide useful information and produce unreliable segmentation or recognition; preprocessing may help, but it also adds computation and cannot recover information that was never captured. Thus an algorithm must balance the input quality, task requirements and available processing time.

### 3.2 SUPPLEMENTARY G6 — lossy vs lossless compression

*IT25 Q1.5, 2 marks.* **Lossless compression** permits exact recovery of the original pixel data; PNG is an example. **Lossy compression** discards some information to reduce size and cannot generally reconstruct the original exactly; ordinary JPEG compression is an example. The distinction is recoverability, not simply whether a compressed image looks visibly worse.

## 4. Enhancement by point processing

*Sir pp.29–57; IT25 Q3(a); A Q1.2/Q2; B Q3(a)/Q3(b).*

Enhancement produces an image more suitable for a particular application. **Spatial-domain methods** operate directly on pixels; **frequency-domain methods** operate on a transformed representation and then return to the image domain. Sir develops spatial methods here.

Let f(x,y) be the input and g(x,y) the output. A spatial operation is written

\[
g(x,y)=T[f(x,y)].
\]

T may use a neighbourhood centred at (x,y). If that neighbourhood is only **1×1**, the output depends on the input pixel alone, giving **point processing**:

\[
s=T(r),
\]

where r and s are input and output gray levels. The same input value receives the same output wherever it occurs. For an 8-bit input, a **lookup table (LUT)** can store the 256 possible output values once, then use each pixel value as an index.

### 4.1 Negative transformation

For levels 0 through L−1, the negative is

\[
s=(L-1)-r.
\]

It reverses brightness order: black becomes white and high input values become low output values. In an 8-bit image, r=50 becomes 255−50=205. It is useful for viewing details whose visibility improves under reversed contrast, including the medical examples mentioned by Sir.

**Curve:** a descending straight line from (0,L−1) to (L−1,0). Sir p.38 explicitly gives L−1−r. The p.39 graphic contains L−f notation without reconciling L; use p.38's stated range/convention rather than producing the invalid level L at r=0.

### 4.2 Logarithmic and inverse-log behaviour

A log transform is

\[
s=c\log(1+r),\qquad c>0.
\]

The 1 makes the mapping defined at zero. The curve rises rapidly at small r and more slowly at large r: relative to the available output range, it separates lower intensities while compressing a large range of high intensities. This helps display data with a large dynamic range. The constant c and log base set the output scale; they must be used consistently. For example, with c=1 and log base 2, r=7 gives s=log₂8=3.

Sir's comparison curve also includes **inverse log**, which has the opposite shape: it compresses the lower part and expands the higher part of the intensity range. Remember the curve distinction; no separate inverse-log numerical is required by the retained PYQs.

### 4.3 Power law and gamma correction

The power-law transformation is

\[
s=cr^\gamma,\qquad c>0,\ \gamma>0.
\]

Gamma changes the shape of the curve. To discuss brightness without confusing scaling, use normalized input r in [0,1] and c=1: **γ<1 raises intermediate values**, **γ=1 is identity**, and **γ>1 lowers intermediate values**. For r=0.25, γ=0.5 gives 0.5, whereas γ=2 gives 0.0625. When working with raw gray levels, follow the question's c and range rather than applying this normalized shortcut blindly.

**Gamma correction** compensates for a display's nonlinear intensity response. Sir's monitor diagram shows that the displayed gradient can differ from the intended gradient; applying a compensating curve before display improves the match. Power-law curves also provide controllable brightening/darkening for enhancement.

| Transformation | Shape/effect to explain in IT25 Q3(a) |
|---|---|
| Negative | Decreasing line; reverses intensity ordering. |
| Logarithmic | Concave increasing curve; expands low-level distinctions and compresses high dynamic range with suitable scaling. |
| Power law | Family controlled by γ; normalized γ<1 brightens, γ>1 darkens. |

**Diagram to remember — pp.37,43–44:** plot output s against input r, add identity, negative, log, and representative power curves; label the gamma cases and the monitor-compensation idea.

### 4.4 Worked power-law numerical — A Q2 / B Q3(a)

Both papers give the same 4×4, 4-bit input and require **g=round(10√f)**:

```text
f = [12  8  4  9]
    [10  5  3  6]
    [ 8 12  9 13]
    [ 4 12  9 10]
```

This is c=10, γ=1/2. Compute the transform for each distinct input value, round the result to the nearest integer, and replace each occurrence. For example, 12 gives 10√12≈34.641→35; 5 gives 22.361→22.

| f | 3 | 4 | 5 | 6 | 8 | 9 | 10 | 12 | 13 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 10√f, approximately | 17.321 | 20 | 22.361 | 24.495 | 28.284 | 30 | 31.623 | 34.641 | 36.056 |
| g after rounding | 17 | 20 | 22 | 24 | 28 | 30 | 32 | 35 | 36 |

```text
g = [35 28 20 30]
    [32 22 17 24]
    [28 35 30 36]
    [20 35 30 32]
```

The question specifies **4-bit input**, not a 4-bit output constraint. It gives no clipping instruction, so do not replace values above 15 by 15. Round after evaluating 10√f, not before multiplication.

### 4.5 Contrast stretching and thresholding

Contrast stretching increases the range occupied by useful gray levels. Sir's piecewise-linear curve passes through (0,0), (r₁,s₁), (r₂,s₂), and (L−1,L−1). Each line segment has its own slope: a slope above 1 expands differences in that interval; below 1 compresses them. The positions of the two internal control points determine which intensities receive increased contrast.

For the nondegenerate case 0<r₁<r₂<L−1, the straight lines in Sir's diagram give

\[
s=\begin{cases}
(s_1/r_1)r,&0\le r\le r_1,\\
s_1+\dfrac{s_2-s_1}{r_2-r_1}(r-r_1),&r_1<r\le r_2,\\
s_2+\dfrac{L-1-s_2}{L-1-r_2}(r-r_2),&r_2<r\le L-1.
\end{cases}
\]

**Small constructed application of the curve:** for L=256, (r₁,s₁)=(50,20) and (r₂,s₂)=(150,220), input r=100 lies in the middle segment. Its slope is (220−20)/(150−50)=2, giving s=20+2(100−50)=120. Do not use the first segment's slope for every pixel.

If r₁=s₁ and r₂=s₂, the curve becomes identity. Sir's limiting case r₁=r₂, s₁=0, s₂=L−1 becomes **thresholding**, which separates pixels into two classes. With the explicit convention “high when r≥T,”

\[
s=\begin{cases}0,&r<T,\\L-1,&r\ge T.\end{cases}
\]

For T=100, inputs 50,100,200 become 0,255,255 in an 8-bit displayed binary image. Treat the threshold as a separate rule; do not divide by r₂−r₁ when those values coincide.

**Diagram to remember — pp.34,46–49:** the piecewise rising curve and its limiting vertical threshold step, with r₁,r₂,s₁,s₂ labelled.

### 4.6 Gray-level slicing

Gray-level slicing highlights an interval of intensities, for example features occupying a selected gray-level band. Sir gives two variants: make the selected interval bright and suppress everything else, or make it bright while retaining the original background intensities. Unlike thresholding's single split, slicing selects a band.

For a constructed interval 80≤r≤160, set selected pixels to 255. Inputs [50,100,200] become **[0,255,0]** when the background is suppressed, and **[50,255,200]** when it is preserved. These examples directly apply the two p.50–52 curves.

**Diagram to remember:** a rectangular high band over [A,B] on a zero background; beside it, the same high band interrupting the identity line. State whether the endpoints belong to the selected band if a numerical gives no convention.

### 4.7 Bit-plane slicing and the retained PYQ

A b-bit pixel is the sum of b binary contributions. Let B_k(x,y) be bit k, with k=0 the least significant bit (LSB):

\[
B_k(x,y)=\left\lfloor\frac{f(x,y)}{2^k}\right\rfloor\bmod2,
\qquad f(x,y)=\sum_{k=0}^{b-1}2^kB_k(x,y).
\]

Each **bit plane** contains that bit from every pixel. Higher bits have larger numerical weights and usually carry the most visible image structure; lower bits contribute finer intensity changes. Sir's 8-bit diagram places plane 0 at the LSB end and plane 7 at the MSB end. Plane 7 is exactly the logical threshold f≥128. The observation that higher planes are more visually significant does not mean lower planes are always noise.

**Worked B Q3(b), 2 marks.** Use the input f from §4.4, not its transformed output g. Write each value as four bits: 12=1100, 8=1000, 4=0100, 9=1001, 10=1010, 5=0101, 3=0011, 6=0110, 13=1101. Reading corresponding bit positions gives:

```text
B3 (weight 8)       B2 (weight 4)
[1 1 0 1]           [1 0 1 0]
[1 0 0 0]           [0 1 0 1]
[1 1 1 1]           [0 1 0 1]
[0 1 1 1]           [1 1 0 0]

B1 (weight 2)       B0 (weight 1)
[0 0 0 0]           [0 0 0 1]
[1 0 1 1]           [0 1 1 0]
[0 0 0 0]           [0 0 1 1]
[0 0 0 1]           [0 0 1 0]
```

Check a location: the top-left bits reconstruct 8×1+4×1+2×0+1×0=12. A bit plane contains **0/1**, not the weighted values 0/8, 0/4, etc. Draw a stack of four or eight 1-bit sheets to explain decomposition visually.

## 5. Histograms and histogram equalisation

*Sir pp.58–83; IPCV Q1.4/Q3(b); B Q1.2.*

### 5.1 What a histogram represents

For gray level r_k, let n_k be its number of occurrences in an image containing N pixels. The **histogram** is h(r_k)=n_k. The **normalized histogram** is

\[
p(r_k)=\frac{n_k}{N},\qquad \sum_kp(r_k)=1.
\]

Normalization turns counts into fractions/probabilities without changing the histogram's shape. A histogram describes the distribution of intensities, not where those intensities occur. Different spatial arrangements may have the same histogram.

Sir's examples relate the distribution to appearance: a dark image concentrates values toward low intensities; a bright image toward high intensities; a low-contrast image occupies a relatively narrow band; a higher-contrast image uses a broader range. The p.69 examples describe the high-contrast case as more evenly spread. This is an interpretation of those images, not a requirement that every high-contrast histogram be flat.

### 5.2 Worked histogram — IPCV Q3(b)

The question supplies the following frequencies. First total them: N=40+45+55+50+40+35+65+70=400. Divide each count by 400.

| Gray level r_k | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| n_k | 40 | 45 | 55 | 50 | 40 | 35 | 65 | 70 |
| p(r_k) | .1000 | .1125 | .1375 | .1250 | .1000 | .0875 | .1625 | .1750 |

The following horizontal bar plots show both distributions; in an exam, put gray level on the horizontal axis and the corresponding count/probability on the vertical axis.

```text
Histogram: each # = 5 pixels       Normalized: each # = 0.0125
0 | ########       40             0 | ########       .1000
1 | #########      45             1 | #########      .1125
2 | ###########    55             2 | ###########    .1375
3 | ##########     50             3 | ##########     .1250
4 | ########       40             4 | ########       .1000
5 | #######        35             5 | #######        .0875
6 | #############  65             6 | #############  .1625
7 | ############## 70             7 | ############## .1750
```

**Source correction:** the PYQ PDF says the histogram “is given as.” The Markdown's “is rising” is a transcription error; the supplied counts are not monotonically increasing. The existing analysis verified the data against the PDF.

### 5.3 SUPPLEMENTARY G2 — mean and standard deviation

The **mean intensity** is a weighted average of gray levels. The **standard deviation** measures their spread about that mean. For the image's full intensity distribution, use population moments:

\[
\mu=\sum_kr_kp(r_k),\qquad
\sigma^2=\sum_k(r_k-\mu)^2p(r_k)
=\sum_kr_k^2p(r_k)-\mu^2,\qquad
\sigma=\sqrt{\sigma^2}.
\]

Continue the same IPCV numerical:

\[
\sum r_kn_k=0+45+110+150+160+175+390+490=1520,
\]
\[
\sum r_k^2n_k=0+45+220+450+640+875+2340+3430=8000.
\]

Therefore **μ=1520/400=3.8**, E[r²]=8000/400=20, **σ²=20−3.8²=5.56**, and **σ≈2.358 gray levels**. Keep enough precision until the final square root; do not average the eight gray-level labels equally or divide by N−1.

For **B Q1.2**, explain that a small standard deviation means intensities are concentrated, whereas a larger one indicates a broader spread and often greater global contrast. It does not by itself establish image quality or spatial detail. The mean describes average brightness, not spread.

### 5.4 Equalisation: why the CDF is used

Histogram equalisation redistributes intensity values to use the available range more effectively. It is useful for many dark, bright or washed-out images. The mapping is based on how much probability has accumulated up to each intensity, called the **cumulative distribution function (CDF)**:

\[
CDF(r_k)=\sum_{j=0}^{k}p(r_j),\qquad
s_k=\operatorname{round}\big[(L-1)CDF(r_k)\big].
\]

The CDF never decreases, so the mapping preserves intensity order, although different input levels may merge. Multiplication by L−1 converts the normalized cumulative value into the output gray-level range; rounding selects an integer level.

**Source convention:** p.71 displays a normalized cumulative sum with its index starting at 1; pp.78–83 use levels starting at 0 and p.80 specifies the rounded integer mapping. The expression above explicitly indexes the bins from 0. Include the probability of gray level 0; do not drop black pixels or multiply by L instead of L−1. No minimum-CDF subtraction is used in Sir's worked example.

### 5.5 Complete equalisation numerical — Sir pp.78–83

For L=8 and N=16, Sir supplies

```text
f = [3 4 5 6]
    [5 4 3 5]
    [6 5 4 5]
    [5 6 4 3]
```

**Step 1: count. Step 2: normalize. Step 3: accumulate. Step 4: scale and round.**

| r_k | n_k | n_k/16 | CDF | 7×CDF | s_k |
|---:|---:|---:|---:|---:|---:|
| 0 | 0 | 0 | 0 | 0 | 0 |
| 1 | 0 | 0 | 0 | 0 | 0 |
| 2 | 0 | 0 | 0 | 0 | 0 |
| 3 | 3 | .1875 | .1875 | 1.3125 | 1 |
| 4 | 4 | .2500 | .4375 | 3.0625 | 3 |
| 5 | 6 | .3750 | .8125 | 5.6875 | 6 |
| 6 | 3 | .1875 | 1.0000 | 7.0000 | 7 |
| 7 | 0 | 0 | 1.0000 | 7.0000 | 7 |

**Step 5: replace each input**, using 3→1, 4→3, 5→6, 6→7:

```text
g = [1 3 6 7]
    [6 3 1 6]
    [7 6 3 6]
    [6 7 3 1]

Output level:  0 1 2 3 4 5 6 7
Output count:  0 3 0 4 0 0 6 3
```

**Step 6: check** that the output still contains 16 pixels and its levels lie in 0–7. The occupied range has spread from 3–6 to 1–7, but the histogram is clearly not flat.

This answers **IPCV Q1.4**: ideal continuous equalisation can redistribute a continuous probability distribution to uniformity under suitable conditions. In a discrete image, whole groups of pixels at the same input level receive one mapped level; integer counts, rounding and possible merging prevent arbitrary redistribution. Consequently equalisation aims to improve range use and contrast, **not guarantee an exactly flat histogram**.

**Diagram to remember — pp.72–83:** input histogram → nondecreasing CDF/mapping curve → output histogram; show that gaps and unequal bars may remain.

## 6. Spatial filtering, smoothing and sharpening

*Sir pp.84–87; IT25 Q3(b); A Q4–Q5; B Q5; IPCV Q4(a).*

### 6.1 Neighbourhood filtering and convolution

A spatial filter computes an output from a small neighbourhood around each pixel. Its **kernel/mask** contains the weights assigned to those neighbours. Weighted averaging suppresses local fluctuations; signed difference weights emphasize changes. Thus the weights determine whether filtering smooths or highlights edges.

For centred offsets u,v and kernel h, **convolution** is

\[
g(i,j)=\sum_u\sum_vh(u,v)f(i-u,j-v).
\]

Here i,j are row/column indices. To execute this as a sliding-window calculation, follow Sir p.84:

1. Flip the supplied kernel in both horizontal and vertical directions, equivalent to a 180° rotation.
2. Place its centre over the output location being computed.
3. Multiply the flipped weights by the overlapping input values and add all products.
4. Repeat at every location. Pad undefined input positions to preserve the image size; use the boundary rule supplied by the problem.

Multiplying by an **unflipped** kernel is correlation. Symmetric mean/Gaussian masks hide the difference, but signed derivative masks may reverse the output sign. Sir's p.86 numerical uses zero-valued positions outside the image.

### 6.2 Complete convolution numerical — Sir p.86

```text
Input f             Kernel h           Flipped h
[1 2 3]             [-1 -2 -1]          [ 1  2  1]
[4 5 6]             [ 0  0  0]          [ 0  0  0]
[7 8 9]             [ 1  2  1]          [-1 -2 -1]
```

The kernel centre is its middle zero. Pad the 3×3 image with one zero border. At the **top-left output**, the neighbourhood is

```text
[0 0 0]
[0 1 2]
[0 4 5]
```

Multiply by the flipped mask: the first row contributes 0, the middle row contributes 0, and the last row contributes −0−2×4−5=**−13**.

At the **centre**, all values are available:

\[
g(1,1)=(1+2\times2+3)-(7+2\times8+9)=8-32=\mathbf{-24}.
\]

At the **top-middle**, only the negative bottom weights contribute: −4−2×5−6=−20. At the **bottom-right**, only the positive top weights contribute: 5+2×6+0=17. Repeating the same placement gives Sir's full output:

```text
g = [-13 -20 -17]
    [-18 -24 -18]
    [ 13  20  17]
```

Keep the signed filter response; no instruction here requires clipping it into a display range. Check the output dimensions, centre placement and flip before doing all nine sums.

### 6.3 Mean and Gaussian smoothing

The **mean filter** replaces a pixel by its neighbourhood average, giving each location equal weight. It reduces rapid local fluctuations but also smooths genuine boundaries and fine detail. A **Gaussian-weighted mask** gives more influence to the centre and nearby positions, producing a smoother weighted average. Sir's 3×3 masks are

```text
Mean: (1/9) ×       Gaussian: (1/16) ×
[1 1 1]             [1 2 1]
[1 1 1]             [2 4 2]
[1 1 1]             [1 2 1]
```

Both have total weight 1, so a constant patch stays constant away from padding effects. **Small application using the p.86 input patch:** the centre mean is 45/9=5; the Gaussian weighted sum is 1+4+3+8+20+12+7+16+9=80, giving 80/16=5. This equality is specific to this patch; the filters generally produce different results. Multiply first, then normalize; omitting 1/9 or 1/16 changes brightness rather than computing the intended average.

### 6.4 SUPPLEMENTARY G1 — 5×5 Gaussian by Pascal's triangle

*A Q1.3, IPCV Q1.3, B Q1.3.* The Pascal row with five entries is **v=[1,4,6,4,1]**. Form the outer product vᵀv, so entry (i,j) equals v_i v_j:

```text
              [ 1  4  6  4  1]
              [ 4 16 24 16  4]
K = (1/256) × [ 6 24 36 24  6]
              [ 4 16 24 16  4]
              [ 1  4  6  4  1]
```

The row sum is 16, so the outer product sums to 16²=256; divide by 256 to normalize. For comparison, [1,2,1] has sum 4 and produces Sir's 3×3 mask with denominator 16. This is the **Pascal/binomial Gaussian approximation** requested by the papers, not a demand to integrate a continuous Gaussian.

### 6.5 SUPPLEMENTARY G4 — why the mean filter is low-pass

*A Q5, proof.* Low spatial frequencies describe slowly varying intensities; high frequencies describe rapid changes. Let n index pixel positions, ω be angular spatial frequency and j be the imaginary unit (j²=−1). For a centred three-point mean, a frequency component e^(jωn) is multiplied by

\[
H(\omega)=\frac{e^{-j\omega}+1+e^{j\omega}}3
=\frac{1+2\cos\omega}{3}.
\]

At zero frequency H(0)=1, so averaging preserves the constant/DC component. Near zero, the gain stays close to 1, preserving slow variation. At the rapidly alternating frequency π, the gain magnitude is only 1/3. Averaging therefore attenuates rapid changes/high-frequency content relative to DC and slow variation, so it acts as a **low-pass filter**.

### 6.6 Derivative and sharpening masks

Derivative filters respond to changes between nearby intensities. Their weights include positive and negative terms and usually sum to zero, so a constant neighbourhood produces zero response. Sir gives two directional masks for both Prewitt and Sobel:

```text
Prewitt, column change   Prewitt, row change
[-1 0 1]                [-1 -1 -1]
[-1 0 1]                [ 0  0  0]
[-1 0 1]                [ 1  1  1]

Sobel, column change     Sobel, row change
[-1 0 1]                [-1 -2 -1]
[-2 0 2]                [ 0  0  0]
[-1 0 1]                [ 1  2  1]
```

Column change responds across left/right regions and helps detect vertical boundaries; row change responds across top/bottom regions and helps detect horizontal boundaries. Sobel gives the central row/column more weight. These are the masks **as printed** on p.87; apply Sir's convolution flip for a numerical rather than changing signs without explanation.

The **Laplacian** uses second differences and combines changes in both image directions. Sir's mask and p.85 sharpening mask are

```text
Laplacian L             Sharpening mask
[0  1 0]                [ 0 -1  0]
[1 -4 1]                [-1  5 -1]
[0  1 0]                [ 0 -1  0]
```

The Laplacian's zero sum suppresses flat background. The sharpening mask has sum 1, retaining a constant background while strengthening local differences.

### 6.7 SUPPLEMENTARY G3 — complete derivative explanations

*A Q4; B Q5; IPCV Q4(a).* For a one-dimensional intensity sequence, a first difference f(x+1)−f(x) measures a local change, while a second difference f(x+1)−2f(x)+f(x−1) measures how that change itself varies. Both vanish on a constant region. Along a constant-slope ramp, the first difference is nonzero but constant, whereas the second is zero except at transitions. Near a sharp step, the second difference gives opposite-signed responses on the two sides.

| First-derivative operators | Second-derivative/Laplacian operator |
|---|---|
| Describe strength and direction of change through directional responses. | Combines second differences; the Laplacian alone does not specify an edge direction. |
| Useful for locating boundaries; Prewitt/Sobel combine differencing with averaging in the other direction. | Useful for highlighting fine changes and constructing sharpening. |
| Still affected by noise; averaging can broaden the response. | Usually more sensitive to noise and may create paired responses around a step. |

For Sir's four-neighbour mask,

\[
\nabla^2 f(i,j)=f(i-1,j)+f(i+1,j)+f(i,j-1)+f(i,j+1)-4f(i,j).
\]

**Restoring background after the Laplacian:** the derivative image alone has lost constant/slow background content. Recombine it with the original image:

\[
g=f-\nabla^2f.
\]

The **minus sign** matches Sir's negative-centre Laplacian. Subtracting its kernel from the identity kernel gives centre 1−(−4)=5 and neighbouring weights −1, exactly the displayed sharpening mask. If a question supplies the opposite Laplacian sign, the recombination sign changes too. This explains IPCV's background-restoration wording without confusing sharpening with a full degradation-inversion method.

## 7. Restoration and noise models

*Sir pp.88–94; filtering/noise portion of IT25 Q3(b).*

**Restoration** aims to recover an image's original content and quality from a degraded observation. It assumes the degradation mechanism is known or can be estimated. **Enhancement** instead aims for a result more suitable for a task or observer; an attractive result need not accurately reproduce the original. Sir emphasizes that “original content and quality” and “good looking” are different objectives.

If f is the original image, h the degradation function, η additive noise and g the observed image, Sir's model is

\[
g(x,y)=h(x,y)*f(x,y)+\eta(x,y),
\]

where * denotes convolution. A restoration operation estimates the original, written \(\hat f\). With noise-only degradation, the task reduces to suitable noise-removal filtering. Sir also shows a frequency route: transform the degraded image, filter/process that representation, then apply the inverse transformation.

**Diagram to remember — pp.88–91:** original f → degradation h → addition of noise η → observed g → restoration → estimated original f̂. Put the noise arrow into the addition junction, not into the original image.

### 7.1 Noise distributions and their appearance

A noise model describes possible noise values through a probability density/distribution. Sir chooses a model using knowledge of the acquisition physics and estimates its parameters from the histogram of a small **flat image region**, where actual scene variation is limited. A whole-image histogram also contains object/background differences and need not directly represent noise.

| Model | Shape to recognize/draw | Source association or observation in Sir |
|---|---|---|
| **Gaussian** | Symmetric bell about mean μ; σ controls spread. | Poor illumination. |
| **Rayleigh** | Starts at a lower limit, rises to a peak, then has a longer right tail. | Range images. |
| **Gamma** | Asymmetric positive-side hump in the illustrated case. | Laser imaging. |
| **Exponential** | Largest at its starting point and decays to the right. | Laser imaging. |
| **Uniform** | Constant height over an interval [a,b], zero outside. | Sir calls it the least used of these models. |
| **Impulse / salt-and-pepper** | Two spikes corresponding to dark and bright impulses. | Faulty switching during imaging; isolated extreme pixels in the example. |

Draw noise value on the horizontal axis and probability/density on the vertical axis. Sir pp.93–94 pair noisy images with histograms: impulse noise produces conspicuous extremes, while other distributions spread intensities in characteristic ways. The source associations are Sir's examples, not exclusive causes of each noise type. The taught emphasis is model recognition and filtering context, not a separate noise-distribution calculation bank.

Mean and Gaussian filters reduce fluctuations by averaging but may blur edges. A filter should match the observed degradation; smoothing is not automatically the best response to every noise model. The small extension below supplies the retained nonlinear-filter PYQs.

### 7.2 SUPPLEMENTARY G5 — order-statistics filters

*A Q1.1/Q7; IPCV Q3(a).* An order-statistics filter sorts neighbourhood values and selects or combines them by rank. In particular, the **median** selects the central ordered value, so a few extreme intensities influence it less than they influence a mean. This is useful for salt-and-pepper noise and often retains boundaries better than ordinary averaging; it is not a linear weighted-sum filter.

| Filter | Rule for sorted values z₁≤…≤z_N | Typical role |
|---|---|---|
| Median | Middle value for an odd-sized window. | Suppress isolated impulse outliers. |
| Minimum | z₁. | Remove isolated bright “salt” values, with possible dark-region expansion. |
| Maximum | z_N. | Remove isolated dark “pepper” values, with possible bright-region expansion. |
| Midpoint | (z₁+z_N)/2. | Estimate a centre value for bounded fluctuations; sensitive to extreme outliers. |
| Alpha-trimmed mean | Discard d/2 lowest and d/2 highest values; average the remaining N−d. | Compromise between averaging and resistance to outliers. |

For alpha trimming, d is an even integer with 0≤d<N:

\[
g=\frac{1}{N-d}\sum_{k=d/2+1}^{N-d/2}z_k.
\]

**One constructed window example:** sorted values [0,10,11,12,13,14,15,16,255] give median=13, minimum=0, maximum=255 and midpoint=127.5. With d=2, discard 0 and 255; the remaining sum is 91, so the alpha-trimmed mean is 91/7=13. The ordinary mean is 346/9≈38.44, illustrating how the bright outlier distorts an average. Trimming d=2 means two values in total, not two from each end.

## 8. SUPPLEMENTARY G8 — warping and geometric transformations

*IT25 Q3(b)/Q4; IPCV Q2(a). This section is a bounded PYQ extension, not a taught matrix chapter.*

**Filtering** calculates intensity values from a pixel or neighbourhood. **Warping** changes where image content is placed by transforming coordinates and resampling the image. Smoothing noise is filtering; shifting, rotating or scaling image content is warping. Warping alone does not remove acquisition noise.

### 8.1 Homogeneous coordinates and matrix order

Represent a Cartesian point as a column vector \(\mathbf p=[x,y,1]^T\). The extra coordinate lets translation and linear transforms be combined by matrix multiplication:

\[
T=\begin{bmatrix}1&0&t_x\\0&1&t_y\\0&0&1\end{bmatrix},\quad
R=\begin{bmatrix}\cos\theta&-\sin\theta&0\\\sin\theta&\cos\theta&0\\0&0&1\end{bmatrix},\quad
S=\begin{bmatrix}s_x&0&0\\0&s_y&0\\0&0&1\end{bmatrix}.
\]

Here θ is positive counter-clockwise in the usual Cartesian axes, t_x,t_y are translations, and s_x,s_y are scale factors. With column vectors, the **rightmost transform acts first**. Translation then rotation then scaling therefore gives \(\mathbf p'=SRT\mathbf p\). Image row coordinates may point downward; do not silently substitute that convention into this explicitly Cartesian CCW question.

### 8.2 Worked IT25 Q4 — 10 marks

Given P=(2,3), translate by (3,−2), rotate 90° CCW about the origin, then scale x by 2 and y by 1:

\[
T=\begin{bmatrix}1&0&3\\0&1&-2\\0&0&1\end{bmatrix},\quad
R=\begin{bmatrix}0&-1&0\\1&0&0\\0&0&1\end{bmatrix},\quad
S=\begin{bmatrix}2&0&0\\0&1&0\\0&0&1\end{bmatrix}.
\]

First multiply the matrices in the required order:

\[
RT=\begin{bmatrix}0&-1&2\\1&0&3\\0&0&1\end{bmatrix},\qquad
SRT=\begin{bmatrix}0&-2&4\\1&0&3\\0&0&1\end{bmatrix}.
\]

Then apply the composite:

\[
\mathbf p'=\begin{bmatrix}0&-2&4\\1&0&3\\0&0&1\end{bmatrix}
\begin{bmatrix}2\\3\\1\end{bmatrix}
=\begin{bmatrix}-2\\5\\1\end{bmatrix}.
\]

Thus **P′=(−2,5)**. Independently check the sequence: (2,3)→(5,1)→(−1,5)→(−2,5). Reversing the matrix order changes the answer because these operations generally do not commute.

### 8.3 Aligning an image to a reference

**Image registration** aligns images of the same scene to a common coordinate system. For IPCV Q2(a), explain the operations: choose corresponding features/points in the reference and the other image; estimate a suitable transformation from those correspondences; transform the moving image's coordinates; resample intensities on the reference grid; check that corresponding structures overlap. Translation, rotation and scaling may suffice for an appropriate image pair. The reference defines the target coordinate system; intensity enhancement alone cannot correct a geometric misalignment.

## 9. Digital video, processing and analytics

*Sir pp.95–102; explicitly within class scope, despite zero supplied PYQ recurrence.*

### 9.1 A video as a spatiotemporal signal

A **digital video** is an ordered sequence of image frames representing changes in objects, the background, or both. Each frame is a 2D image. Once time is included, the video is a **3D spatiotemporal signal**, V(x,y,t), where x,y identify a position and t identifies a time/frame. This does not mean the video automatically contains 3D scene geometry.

**Sir's p.97 example:** a 1920×1080 video with 100 frames has array dimensions 1920×1080×100, or **207360000 spatial–temporal sample locations** for one value per location. These are samples, not bytes; storage additionally depends on channels, bit depth and compression. Draw several 2D frames stacked along a time axis to explain the representation.

### 9.2 Processing stages and operations

The p.98 workflow begins with **acquisition**, then **sampling** into discrete spatial/temporal measurements and **quantization** into intensity levels. **Compression** reduces data for **storage/transmission**, and **display/playback** reconstructs a visible sequence. Each stage has a distinct role: sampling decides where/when measurements exist; quantization decides which intensity values are representable.

**Spatial processing** operates within frames, such as filtering, enhancement and edge detection. **Temporal processing** compares frames over time, such as frame differencing or motion estimation. **Motion analysis** detects or tracks moving objects. Video enhancement improves frame quality; video segmentation separates regions/foreground; video compression reduces redundancy within a frame (**intra-frame**) or between frames (**inter-frame**). Sir illustrates surveillance, traffic monitoring, sports and other video applications rather than requiring a separate algorithm for each.

### 9.3 Video processing vs video analytics

Video processing mainly modifies the signal; video analytics extracts information about what is happening. Processing may therefore supply cleaner frames to analytics, but a processed image and an interpreted event are different outputs.

| Aspect | Video processing | Video analytics |
|---|---|---|
| Main purpose | Improve, transform or manipulate video. | Extract information and support decisions. |
| Focus | Pixels and frames. | Objects, events and behaviour. |
| Operations | Filtering, enhancement, compression, resizing, stabilization, frame extraction. | Detection, tracking, classification, activity recognition. |
| Output | Modified video or frames. | Counts, events, alerts, statistics or decisions. |
| AI requirement | Not necessarily AI-based. | Frequently uses AI/ML/DL. |
| Example | Remove noise or resize 4K video to HD. | Detect a restricted-area entry or count vehicles. |

### 9.4 Visual and intelligent surveillance

**Object detection** locates objects in a frame; **object tracking** maintains their association over time. Sir's basic visual-surveillance system combines both, so it can use a sequence rather than unrelated individual detections.

```text
CCTV sequence → object detection + object tracking → surveillance information

Video capture → preprocessing/features → spatiotemporal modelling
              → anomaly/intrusion detection → alerts → monitoring/response
```

In the expanded p.102 pipeline, preprocessing reduces nuisance variation and extracts useful features. Spatiotemporal modelling uses appearance and motion across a sequence to describe behaviour. Detection identifies an intrusion or departure from expected behaviour; alert generation communicates it, and monitoring/response uses the result. For a theory answer, connect these functions instead of merely writing that surveillance “uses AI.”

## 10. Object detection and tracking methods in Sir's notes

*Sir pp.103–114. The following is the taught method/diagram depth; formulas alone are not evidence of a likely numerical.*

### 10.1 Object detection by background modelling

Background modelling learns what the scene normally looks like, typically from a static camera, and detects regions that differ from that model. Let I_t(x,y) be the current frame and B_t(x,y) the background estimate. Sir p.103 shows

\[
D_t(x,y)=|I_t(x,y)-B_t(x,y)|,\qquad
M_t(x,y)=\begin{cases}1,&D_t(x,y)>T,\\0,&\text{otherwise}.\end{cases}
\]

T is a difference threshold and M_t is a binary foreground mask. Clean the mask to remove noise/fill holes, then localize objects, for example with bounding boxes, area and centroid. Sir names erosion/dilation, opening/closing, hole filling and connected-component processing in this cleanup stage; their role here is mask cleanup/grouping, not a separate set of morphology numericals.

A simple background update on the same slide is the **running average**:

\[
B_t=(1-\alpha)B_{t-1}+\alpha I_t,\qquad0<\alpha<1.
\]

Alpha is the learning rate: a small value retains more of the previous background and adapts slowly; a larger value responds faster to recent observations. The model can accommodate gradual changes rather than treating every small change as a new object.

**Minimal constructed application of p.103's equations:** if one pixel has B_(t−1)=20, I_t=30 and α=0.1, then B_t=0.9×20+0.1×30=21. Using this updated estimate, D_t=|30−21|=9; with T=8, M_t=1. A question must make clear which background estimate is used. Follow its update/detection order.

**Diagram:** frames → background model → difference image → thresholded mask → cleaned mask → detected object. Sir lists running average, GMM, kernel-density and codebook methods as possible background models; the developed alternative here is GMM in §10.4.

### 10.2 Object detection by object modelling

Object modelling represents the **target's appearance**, then searches for it in a new image. Collect views of the target under different conditions, align/normalize the examples, extract distinguishing features, and build a model/template. Extract features from candidate regions in the new image, compare them with the model, and localize sufficiently good matches.

Sir p.104 names colour histograms, HOG, SIFT/SURF/ORB and CNN features as representation examples, and SSD, normalized cross-correlation, cosine similarity and chi-square distance as comparison examples. The required concept is the **representation → search → match → localization** pipeline. In the slide's similarity-score illustration, 0.86 is the strongest candidate among 0.12,0.18,0.86,0.21,0.15 and passes the chosen threshold. The slide's “higher is better” wording applies to similarity scores; a raw difference measure such as SSD is better when smaller.

The key distinction is what is modelled: **background modelling asks what differs from the normal scene; object modelling asks what matches the target**. Draw the first with a background image and foreground mask, and the second with a target template and candidate boxes.

### 10.3 Frame differencing

Frame differencing detects change by comparing consecutive frames, without requiring a persistent background model. Sir p.106 defines

\[
D_t(x,y)=|I_t(x,y)-I_{t-1}(x,y)|,\qquad
B_t(x,y)=\begin{cases}1,&D_t(x,y)\ge T,\\0,&\text{otherwise}.\end{cases}
\]

Here B_t denotes a **binary mask**, whereas p.103 used B_t for a background estimate. Also note p.106's **≥T**, versus p.103's **>T**: use the rule given with the method/problem. The absolute difference measures the amount of change in either direction; plain signed subtraction would miss some darkening changes under a positive threshold.

The workflow is frames → absolute difference → threshold → postprocessing → object detection. Opening/closing can remove small noise and improve the detected mask. The method is simple, fast and useful for a static background with moving objects, but camera noise or illumination changes can also create differences. It detects changed regions, which need not be a complete object silhouette.

**Minimal constructed frame numerical**, applying Sir's rule with T=5:

```text
I_(t−1) = [10 10 20]     I_t = [12 18 15]
           [10 30 30]           [10 24 35]

D_t     = [ 2  8  5]     B_t = [0 1 1]
           [ 0  6  5]           [0 1 1]
```

For example |24−30|=6 is foreground, and a difference exactly 5 is foreground because the condition is ≥5. This illustrates the taught procedure; it is not a supplied PYQ prediction.

### 10.4 Multi-frame intruder detection and GMM

**Two/three-frame illustration — p.109.** A moving object occupies different positions in successive frames. A difference of two frames can highlight both vacated and newly occupied regions. Combining change masks from successive pairs keeps common change evidence, but the illustrated three-frame result can still contain only part of the object. Sir's five-frame scheme adds further mask combinations to recover more of the target-frame region.

**Five-frame procedure — p.110.** Take I_(t−2), I_(t−1), I_t, I_(t+1), I_(t+2). Let G_(a,b) denote the binary change mask from a neighbouring frame pair. The slide combines these masks as follows. In its binary-mask diagram, `·` denotes intersection/AND and `+` combines masks as union/OR; these are not unbounded grayscale sums.

```text
For j = t−1, t, t+1:
  GA_j = G_(j−1,j) · G_(j,j+1)
  GO_j = G_(j−1,j) + G_(j,j+1)
  GD_j = |GO_j − GA_j|

GE_(t−1) = GD_(t−1) · GD_t
GE_(t+1) = GD_t · GD_(t+1)
GM_(t−1) = G_(t−1,t) + GE_(t−1)
GM_(t+1) = G_(t,t+1) + GE_(t+1)
GS_(t−1) = |GM_(t−1) − G_(t−1,t)|
GS_(t+1) = |GM_(t+1) − G_(t,t+1)|
O_t = GS_(t−1) + GA_t + GS_(t+1)
```

O_t is the resulting change-detection mask for frame I_t. The diagram's logic is to combine pairwise overlap, difference and recovered side regions, then join them into a target-frame mask. **Diagram to remember:** five frames → four pair masks G → GA/GO → GD → GE → GM/GS → O_t. The slide refers to equation numbers from its cited paper for initial differences/thresholds without reproducing those equations; the exact paper-specific initialization is not supplied. Preserve the displayed mask procedure rather than inventing a threshold or researching the paper.

**Gaussian Mixture Model (GMM) — p.111.** A single pixel may legitimately take several background appearances over time, for example because underwater vegetation moves or illumination varies. One fixed background value is then inadequate. Sir models the pixel with **multiple adaptive Gaussian distributions** so that several recurring appearances can belong to the background. Values that do not fit the background distributions are classified as foreground. Draw several Gaussian humps for a pixel's possible background values; explain why multiple modes are useful. No parameter-update derivation is supplied in this slide.

### 10.5 Wronskian Change Detection Model

*Sir p.112.* This is a **vector image model** for detecting changes between frames. Instead of representing a pixel using only its own intensity, include its **region of support**: the illustrated 3×3 neighbourhood is arranged as a nine-component vector. The model thus includes **spatio-contextual** information, meaning information from the pixel's surrounding region.

Let \(\vec F_t(x,y)_i\) denote component i of the support vector at time t and n its number of components. Defining the component ratio \(q_i=\vec F_t(x,y)_i/\vec F_{t-1}(x,y)_i\), the expression printed on Sir's slide is

\[
|W|=\frac1n\sum_{i=1}^{n}(q_i^2-q_i).
\]

If corresponding nonzero components are unchanged, each ratio is 1 and contributes zero. **Source limitation:** the slide labels the result |W| although the displayed right-hand side is not necessarily nonnegative; it also does not state a zero-denominator rule or decision threshold. This reproduces the supplied expression, without silently replacing it. Prepare the model's purpose, support-vector diagram and printed formula as theory, not an invented worked numerical.

**Diagram:** mark a centre pixel → draw its 3×3 support → list those nine pixel values as a column vector → compare vectors from two frames. Keep the ordering identical across frames.

### 10.6 Crowd clustering and particle-filter tracking

**Clustering/reassigning — p.113.** Sir illustrates 13 detected blobs grouped by a GMM with k=3. Grouping puts blobs with related features into clusters, which supports distinguishing candidate regions before tracking/reassignment. **Slide illustration only (not for memorization):** the displayed groups are C₁={F₅,F₇}, C₂={F₁,F₃,F₈,F₁₀}, and C₃={F₂,F₄,F₆,F₉,F₁₁,F₁₂,F₁₃}, with cluster density increasing down the diagram. Remember the grouping/reassignment idea and the three-group diagram; the slide does not supply a full clustering optimization procedure.

**Particle filter framework — p.114.** Tracking maintains a description of an object's motion over time. Sir writes the state as

\[
S_{t-1}=\{x_c,y_c,v_x,v_y,a_x,a_y\},
\]

where x_c,y_c locate the object centre, v_x,v_y describe velocity and a_x,a_y acceleration. A particle representation keeps multiple candidate states/locations to represent uncertainty, rather than assuming one exact position. The diagram shows particles and a window at t−1, followed by candidate windows/centres at t. Explain how the location and motion description help follow an object into the next frame. Draw the two time instants and candidate windows; no weight/resampling equations or new tracking numerical are required at the supplied slide depth.

## 11. Detection architecture and CNN workflow

*Sir pp.115–121. CORE at the overview depth taught here.*

### 11.1 Backbone, neck and detection head

Sir's general deep-learning detection architecture separates three jobs. The **backbone** extracts hierarchical feature maps from the image, ranging from local visual patterns to richer object-related representations. The **neck** combines features across levels/scales so that objects of different sizes can be detected while retaining useful spatial information. The **detection head** uses these features to predict an object's class, bounding box and objectness/confidence.

```text
Input image → backbone (feature extraction) → neck (feature aggregation)
            → detection head (class + box + objectness)
            → confidence filtering and NMS → final detections
```

The input is resized before processing. Sir gives a bounding box as (x,y,w,h): position and size. The final stage uses a confidence threshold and **Non-Maximum Suppression (NMS)** to suppress redundant competing detections and produce the final boxes. This is the stage's role; a separate NMS calculation is not taught here.

| Neck | Full form and role from p.118 |
|---|---|
| **FPN** | **Feature Pyramid Network**: combines higher-level semantic features with lower-level spatial features for detecting objects at different scales. |
| **PAN** | **Path Aggregation Network**: adds a bottom-up path to improve the flow of localization/low-level information. |
| **BiFPN** | **Bidirectional Feature Pyramid Network**: repeats top-down and bottom-up fusion with learnable weights for efficient multi-scale aggregation. |

Sir p.116 associates **YOLO and Faster R-CNN** with object detection, **DeepSORT** with tracking, **3D CNNs/LSTM/Transformers** with temporal modelling, and **autoencoders/GANs** with anomaly detection. Learn those task associations; their internal architectures are not developed in this section of the supplied notes.

### 11.2 Working of a CNN model

A **Convolutional Neural Network (CNN)** learns hierarchical features from images and uses them for a task such as classification. Sir's repeated p.119–121 workflow shows a hand image passing through convolution, activation, pooling, flattening, fully connected layers and softmax. It explains how an array becomes a class prediction:

1. **Input:** represent the image numerically; the illustration uses 128×128×1, a single-channel input.
2. **Convolution:** slide small filters over local regions and multiply/add values to form feature maps. Different filters capture patterns such as edges, lines and textures.
3. **ReLU activation:** replace negative responses by zero using \(\operatorname{ReLU}(z)=\max(0,z)\). This introduces nonlinearity so the network can represent more than a sequence of linear operations.
4. **Max pooling:** keep the largest value from each small region, reducing spatial size and computation while retaining strong responses. Sir illustrates \(\begin{bmatrix}4&7\\1&3\end{bmatrix}\to7\); this is a workflow illustration, not a separate exam numerical.
5. **Flatten:** arrange the remaining feature-map entries into a one-dimensional feature vector.
6. **Fully connected layers:** combine the extracted features to produce class-related scores.
7. **Softmax output:** convert scores into class probabilities whose sum is 1; select the largest as the predicted class. Sir's illustration has 0.92 for “fractured” and 0.08 for “non-fractured.”

**Diagram to remember:** image → convolutional feature maps → ReLU → pooled maps → flattened vector → fully connected layers → class probabilities. The learned hierarchy in Sir's summary is **edges → textures → parts → objects → classification**. Convolution extracts local information, pooling reduces its spatial size, and the final layers combine it for the decision; these operations should not be described as interchangeable.
