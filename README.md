# Image Compressor by PCA

A lightweight implementation of digital image compression using **Principal Component Analysis (PCA)** from scratch with Python and NumPy. This project demonstrates how 3D RGB color channels can be projected onto a 2D subspace to reduce data dimensionality while preserving the primary color distribution and visual details.

---

## Features

- **Dimensionality Reduction**: Projects 3D RGB pixel color data into 2 principal components.
- **From-Scratch Implementation**: Built using fundamental linear algebra routines (mean-centering, sample covariance matrix calculation, and eigendecomposition) without relying on black-box machine learning libraries.
- **Reconstruction & Comparison**: Reconstructs compressed 2D coordinate projections back into 3D RGB space and provides side-by-side visual comparisons against the original images.
- **Sample Images Included**: Pre-configured with sample test assets (`test.jpg`, `colorfull.jpg`) and their reconstructed counterparts.

---

## Repository Structure

```plaintext
Image-compressor-by-PCA/
│
├── Image_compressor.ipynb        # Main Jupyter Notebook with step-by-step implementation
├── test.jpg                      # Sample input image
├── test_reconstructed.jpg        # Output reconstructed image from test.jpg
├── colorfull.jpg                 # Vibrant sample input image
├── colorfull_reconstructed.jpg   # Output reconstructed image from colorfull.jpg
└── README.md                     # Project documentation
```

---

## Mathematical Workflow

1. **Data Representation**:
   An input image of shape $(H \times W \times 3)$ is reshaped into a 2D matrix $X \in \mathbb{R}^{N \times 3}$, where $N = H \times W$ (total pixels) and columns represent the Red, Green, and Blue intensity channels.

2. **Mean Centering**:
   The mean vector $\mu \in \mathbb{R}^{1 \times 3}$ is computed across all pixel samples and subtracted:
   $$X_{\text{centered}} = X - \mu$$

3. **Covariance Matrix**:
   The $3 \times 3$ covariance matrix $\Sigma$ is calculated:
   $$\Sigma = \frac{1}{N - 1} X_{\text{centered}}^T X_{\text{centered}}$$

4. **Eigendecomposition & Component Selection**:
   The eigenvalues $\lambda_i$ and corresponding eigenvectors $v_i$ are computed:
   $$\Sigma v = \lambda v$$
   The eigenvectors are sorted in descending order of eigenvalue magnitudes. The top $k = 2$ eigenvectors form the projection matrix $W \in \mathbb{R}^{3 \times 2}$.

5. **Projection (Compression)**:
   The centered RGB data is projected onto the 2D subspace:
   $$Z = X_{\text{centered}} W \quad (Z \in \mathbb{R}^{N \times 2})$$

6. **Reconstruction (Decompression)**:
   The compressed data is projected back to 3D RGB space and shifted by the mean vector:
   $$X_{\text{reconstructed}} = Z W^T + \mu$$
   Pixel intensities are clipped to $[0, 1]$ (or $[0, 255]$) to ensure valid image display.

---

## Prerequisites & Installation

### Requirements
- Python 3.8+
- Jupyter Notebook / JupyterLab

### Install Dependencies
```bash
pip install numpy pillow matplotlib
```

---

## Usage

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/getabalewshimelis/Image-compressor-by-PCA.git](https://github.com/getabalewshimelis/Image-compressor-by-PCA.git)
   cd Image-compressor-by-PCA
   ```

2. **Launch Jupyter Notebook:**
   ```bash
   jupyter notebook
   ```

3. **Run the Notebook:**
   Open `Image_compressor.ipynb` and execute the cells sequentially to load an image, perform PCA compression, and visualize the reconstructed output.


## Contributing

Contributions, issues, and feature requests are welcome. Feel free to open an issue or submit a pull request.
