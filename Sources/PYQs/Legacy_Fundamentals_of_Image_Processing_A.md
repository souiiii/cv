# Legacy Fundamentals of Image Processing Mid-Semester Paper A

Source: page 4 of the supplied `7thSem_lib_pyqs.pdf` bundle.

Historical paper from IIIT Bhubaneswar, 7th semester ETC, subject `Fundamentals of Image Processing`. It is **not the same current IT Computer Vision course**, so use it only for overlapping image-processing question patterns.

- Full marks: 30
- Duration: 90 minutes
- Instruction: Answer any six questions including Q1. All questions carry equal marks.

## Questions

### Question 1
1. What is alpha-trimmed mean filter?
2. Explain power-law transformation with its applications.
3. Determine a 5 × 5 Gaussian kernel using Pascal's triangle method.

### Question 2
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

### Question 3
1. Explain m-adjacency and its advantage with an example.
2. For the supplied image segment and `V={1,2}`, compute the lengths of the shortest 4-, 8-, and m-paths between p and q.

### Question 4
Describe first-order and second-order derivative image-sharpening filters, with their advantages and disadvantages.

### Question 5
Prove that the mean/average filter used in image processing is a low-pass filter.

### Question 6
What conditions must be satisfied by distance measures? Explain various distance measures between two pixels.

### Question 7
Explain order-statistic filters with their applications.

## Use in this project

Relevant overlap with Sir's current notes: power-law/intensity transformation, Gaussian/mean filtering, derivative sharpening/filter kernels. Adjacency, distance measures and order-statistic-filter material should remain **secondary/gap material** unless supported by current notes or reliable class guidance.
