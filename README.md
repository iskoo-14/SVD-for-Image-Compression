# SVD for Image Compression

**Computational Linear Algebra – Academic Year 2024–2025**  
**Authors:** Ismail Aljosevic (s337769), Daniele Amato (s334211)

## 📌 Project Overview

This project explores the application of **Singular Value Decomposition (SVD)** for RGB image compression.

The main objective is to reduce image storage requirements using low-rank matrix approximation while preserving acceptable visual quality.

We analyze how varying the number of singular values `k` affects:

- Image reconstruction quality  
- Energy retention  
- Compression efficiency
  
⚠️ **The complete implementation, experiments, visualizations, and results are entirely contained in `software.ipynb`.**

## 📚 Theoretical Background

### 🔹 Singular Value Decomposition (SVD)

For a matrix:

$$
A \in \mathbb{R}^{m \times n}
$$

the Singular Value Decomposition is defined as:

$$
A = U \Sigma V^T
$$

Where:

- `U` – orthogonal matrix of left singular vectors  
- `V` – orthogonal matrix of right singular vectors  
- `Σ` – diagonal matrix containing singular values  
- Singular values are ordered as:

$$
\sigma_1 \geq \sigma_2 \geq \dots \geq \sigma_r > 0
$$

Each triplet `(σᵢ, uᵢ, vᵢ)` represents a fundamental component (mode) of the matrix.


### 🔹 Low-Rank Approximation

A matrix can be approximated using only the first `k` singular values:

$$
A_k = \sum_{i=1}^{k} \sigma_i u_i v_i^T
$$

This gives the **best rank-k approximation** in terms of reconstruction error.

Most of the matrix energy is typically concentrated in the first few singular values, which enables compression.


## 🖼 Image Compression Strategy

An RGB image consists of three channels:

- Red
- Green
- Blue

Each channel is treated as an independent matrix.

### Steps:

1. Load an RGB image  
2. Convert it into a NumPy array  
3. Normalize pixel values between 0 and 1  
4. Apply `np.linalg.svd()` to each channel  
5. Reconstruct the image using only the first `k` singular values  
6. Evaluate visual quality and cumulative energy  


## 📊 Experimental Results

- Image resolution: **1080 × 1080 × 3**
- Singular values show a sharp decay in the first 3–5 components.
- Cumulative energy was evaluated at:
  - 90%
  - 95%
  - 99%

### 🔹 Key Findings

| Energy Threshold | Required k | Result |
|-----------------|------------|--------|
| 95%             | k ≈ 15     | Recognizable but blurry image |
| 99%             | k ≈ 120    | Clear and visually satisfying reconstruction |
| ~Full quality   | k ≈ 600    | Almost identical to original |

Additional observations:

- The **blue channel** required more singular values to reach the same energy threshold.
- Retaining 99% of the energy offers an excellent trade-off between compression and image clarity.
- Singular values decay rapidly at first, then gradually, with a sharper drop around k ≈ 500–600.


## 💾 Compression Insight

Original storage per channel:

$$
m \times n
$$

Compressed storage per channel:

$$
k(m + n + 1)
$$

Compression is effective when:

$$
k(m + n + 1) < mn
$$


## 🛠 Technologies Used

- Python  
- NumPy  
- Matplotlib  
- Pillow  
- Linear Algebra (SVD theory)




