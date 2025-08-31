

# Deep Image Steganography

## Overview

**Deep Image Steganography** is a lightweight PyTorch-based project that **hides a secret image inside a cover image** and later recovers it. Using **weighted blending**, it maintains high visual fidelity while enabling image steganography in an end-to-end pipeline.

* Supports **batch processing** with PyTorch DataLoader.
* Computes **image quality metrics** such as SSIM and MSE.
* Provides **visualizations** for cover, secret, encoded, and decoded images.

---

## Features

* **Encode & Decode:** Hide a secret image in a cover image with a simple weighted blending approach.
* **Evaluation Metrics:**

  * **SSIM:** Structural similarity between original and decoded images.
  * **MSE:** Pixel-wise difference.
* **Visualization:** Compare original, encoded, and decoded images side-by-side.
* **Flexible Dataset:** Works with **Flickr8k** or custom image datasets.

---

## Installation

Clone the repository:

```bash
git clone https://github.com/shrinkhlap/deep-image-steganography.git
cd deep-image-steganography
```

Install dependencies:

```bash
pip install -r requirements.txt
```

**requirements.txt:**

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

* Uses the **Flickr8k dataset**.
* Images are loaded from a folder and resized to **512×512**.
* Custom PyTorch `Dataset` implementation:

```python
dataset = Flickr8kDataset("/path/to/Flickr8k/Images", transform=transform)
dataloader = DataLoader(dataset, batch_size=2, shuffle=True)
```

---

## Usage

### 1. Encode and Decode

```python
encoded_image = encode_stegano(cover_image, secret_image, alpha=0.1)
decoded_secret_image = decode_stegano(encoded_image, cover_image, alpha=0.1)
```

### 2. Visualize

```python
show_images(
    [cover_image[1], secret_image[1], encoded_image[1], decoded_secret_image[1]],
    ["Cover", "Secret", "Encoded", "Decoded Secret"]
)
```

### 3. Evaluate

```python
ssim_score, mse_score = calculate_metrics(secret_image[1], decoded_secret_image[1])
print(f"SSIM: {ssim_score:.4f}, MSE: {mse_score:.4f}")
```

---

## Methodology

1. **Encoding:** Blend secret into cover:

```python
encoded = (1 - alpha) * cover + alpha * secret
```

2. **Decoding:** Recover secret:

```python
decoded = (encoded - (1 - alpha) * cover) / alpha
decoded = torch.clamp(decoded, 0, 1)
```

3. **Evaluation:**

   * **SSIM**: Structural similarity between original and decoded images.
   * **MSE**: Pixel-wise difference between images.


## License

This project is licensed under the **Apache 2.0 License**.



Do you want me to do that?
