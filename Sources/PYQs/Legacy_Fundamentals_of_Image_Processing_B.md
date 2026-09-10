# Legacy Fundamentals of Image Processing Mid-Semester Paper B

Source: page 20 of the supplied `7thSem_lib_pyqs.pdf` bundle.

Historical IIIT Bhubaneswar paper for 7th semester ETC, subject `ET124: Fundamentals of Image Processing`. It is **not the same current IT Computer Vision course**, so use it only as secondary evidence for overlapping question patterns.

- Full marks: 30
- Duration: 90 minutes
- Instruction: Answer any five questions including Q1. All questions carry equal marks.

## Question 1 — [2 × 3 = 6]

1. Prove that the 1D DFT transform matrix is unitary and symmetric.
2. What does the standard deviation of a histogram tell us about the image?
3. Determine a 5 × 5 Gaussian kernel using Pascal's triangle method.

## Question 2 — [6]

Explain the types of images formed based on radiation from the electromagnetic spectrum.

## Question 3 — [4 + 2 = 6]

### 3(a)
A 4 × 4, 4-bits/pixel image `f(m,n)` is passed through the point intensity transformation

`g(m,n) = round(10 × √f(m,n))`.

Determine the output image `g(m,n)` when

```text
f(m,n) =
[12  8  4  9]
[10  5  3  6]
[ 8 12  9 13]
[ 4 12  9 10]
```

### 3(b)
Find the four bit planes of the given image `f(m,n)`.

## Question 4 — [3 + 3 = 6]

### 4(a)
Explain m-adjacency and its advantage with an example.

### 4(b)
For the supplied image segment and `V={1,2}`, compute the lengths of the shortest 4-, 8-, and m-paths between the marked points.

## Question 5 — [3 + 3 = 6]

Explain first-order derivative and second-order derivative image-sharpening filters.

## Question 6 — [4 + 2 = 6]

Explain the Hadamard Transform. Generate the transformation matrix for `N=8` using the mathematical equation and also using the Kronecker product method.

## Use in this project

Relevant overlap with Sir's current notes: histogram concepts, Gaussian kernels, point intensity transformations, bit-plane slicing and derivative/sharpening filters. DFT, adjacency/path distance and Hadamard-transform material should remain secondary/gap material unless supported by current notes or reliable class guidance.
