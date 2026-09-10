# Legacy Image Processing and Computer Vision Mid-Semester Paper

Source: page 10 of the supplied `7thSem_lib_pyqs.pdf` bundle.

Historical IIIT Bhubaneswar paper for 7th semester ETC, subject `Image Processing and Computer Vision`. It is **not the same current IT course**, so use it only as secondary evidence for overlapping image-processing question styles.

- Full marks: 30
- Duration: 90 minutes
- Instruction: Answer any three questions including Q1. All questions carry equal marks.

## Question 1 — [2 × 5 = 10]

1. How is an image represented using illumination and reflectance components?
2. What are the categories of images generated due to different energy sources from the electromagnetic spectrum?
3. Generate a 5 × 5 Gaussian kernel using Pascal's triangle method.
4. Explain why the discrete histogram equalization technique does not yield a flat histogram in general as the continuous histogram technique does.
5. What is chessboard distance?

## Question 2 — [5 + 5]

### 2(a)
Two images of the same scene are given. One is a reference image. What transformation technique can be used to align both images? Explain the operations in detail.

### 2(b)
For the supplied image segment and `V={0,1}`, determine the 4-adjacency. Compute the lengths of the shortest 4-, 8-, and m-paths between the marked points if the paths exist.

## Question 3 — [5 + 5]

### 3(a)
What are various order-statistics filters? Explain with an example.

### 3(b)
An image has gray levels from 0 to 7 with the following frequencies:

```text
Gray level:  0  1  2  3  4  5  6  7
Frequency:  40 45 55 50 40 35 65 70
```

Plot the histogram and normalized histogram. Using the normalized values, compute the mean and standard deviation of the image. The histogram is rising.

## Question 4 — [5 + 5]

### 4(a)
Explain the Laplacian operator with its application. How can the background features of an image be restored after performing the Laplacian operator?

### 4(b)
Explain homomorphic filtering. Also explain which filter can be used to gain control over both the illumination and reflectance components.

## Use in this project

Strong overlap with Sir's current notes: Gaussian kernels/filtering, histogram equalization, histogram numericals, Laplacian, image restoration, and illumination-related image formation. Adjacency, chessboard distance, order-statistics filters, homomorphic filtering and registration/alignment should be treated as secondary unless current-source evidence supports them.
