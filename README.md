#  Deep Image Steganography with DDPM & Stable Diffusion

## Overview

**Deep Image Steganography** leverages **Denoising Diffusion Probabilistic Models (DDPM)** and **Stable Diffusion** to securely embed secret data within images. The system achieves **high-fidelity image concealment**, ensuring imperceptible quality loss while maintaining robustness against detection.

* Combines **diffusion-based generative modeling** with neural architectures for optimized information hiding.
* End-to-end pipeline: **encode → embed → decode**.
* Visualizes cover, secret, encoded, and decoded images for easy interpretation.

---

## Features

* **High-Fidelity Embedding:**

  * Achieved **SSIM: 99.82%** and **MSE: 0.4282** on secret image recovery.
* **Diffusion-Based Generative Modeling:** Uses DDPM and Stable Diffusion for imperceptible steganography.
* **Visualization:** Compare cover, secret, encoded, and decoded images side by side.
* **Custom Dataset Support:** Works with **Flickr8k** or any folder of RGB images.

---

## Installation

Clone the repository:

```bash
git clone https://github.com/shrinkhlap/Deep-image-steganography_Stable-Diffusion.git
cd Deep-image-steganography_Stable-Diffusion
```

Install dependencies:

```bash
pip install -r requirements.txt
```

**requirements.txt**

```text
torch>=2.0.0
torchvision>=0.15.0
numpy>=1.23.0
matplotlib>=3.5.0
Pillow>=9.0.0
opencv-python>=4.7.0
scikit-image>=0.20.0
diffusers>=0.19.0
```

---

## Dataset

* Supports **Flickr8k** or custom datasets.
* Images are resized to **512×512**.

```python
dataset = Flickr8kDataset("/path/to/Flickr8k/Images", transform=transform)
dataloader = DataLoader(dataset, batch_size=2, shuffle=True)
```

---

## Usage

### 1. Encode Secret Image

```python
encoded_image = encode_stegano(cover_image, secret_image, alpha=0.1)
```

### 2. Decode Secret Image

```python
decoded_secret_image = decode_stegano(encoded_image, cover_image, alpha=0.1)
```

### 3. Visualize Results

```python
show_images(
    [cover_image[1], secret_image[1], encoded_image[1], decoded_secret_image[1]],
    ["Cover", "Secret", "Encoded", "Decoded Secret"]
)
```

### 4. Evaluate Performance

```python
ssim_score, mse_score = calculate_metrics(secret_image[1], decoded_secret_image[1])
print(f"SSIM: {ssim_score:.4f}, MSE: {mse_score:.4f}")
```

---

## Methodology

1. **Diffusion-Based Encoding:**

   * Secret image is embedded into cover image using **DDPM** to ensure imperceptibility.
   * Stable Diffusion helps optimize spatial patterns for secure data hiding.

2. **Decoding:**

   * Extracts the secret image using inverse operations while preserving high fidelity.

3. **Evaluation Metrics:**

   * **SSIM (Structural Similarity Index):** Measures perceptual similarity.
   * **MSE (Mean Squared Error):** Measures pixel-level differences.


## License

This project is licensed under the **Apache License 2.0**.


