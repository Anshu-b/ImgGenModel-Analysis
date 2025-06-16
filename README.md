# ImgGenModel-Analysis: Comparative Analysis of Stable Diffusion and Conditional DC-GANs  
### A Multi-Dataset Evaluation Framework  
**Authors:** Ansh Bhatnagar, Jeronimo Adames-Baena  
**Date:** June 16, 2025

## Overview

This project presents a comparative analysis between two state-of-the-art generative image models—**Stable Diffusion** and **Conditional DC-GANs (cDC-GANs)**—across two datasets: **CelebA** and **CIFAR-10**. Our goal was to evaluate how well each model performs in terms of perceptual quality, attribute fidelity, prompt control, and downstream machine learning utility.

---

## Objectives

- Evaluate image generation quality across fine-grained attributes (e.g., gender and bangs).
- Benchmark conditional GANs with multiple optimizers (Adam, RMSProp) and loss functions (BCEWithLogits, Hinge).
- Assess tradeoffs between zero-shot diffusion models and from-scratch trained GANs.
- Highlight practical limitations in training efficiency, dataset access, and hardware resources.

---

## Datasets

### CelebA
- ~200,000 images of celebrity faces.
- Used 2x2 categorical conditioning: `{male, female} × {with bangs, without bangs}`.
- Images resized to 64x64 and normalized.

### CIFAR-10
- 60,000 32x32 color images across 10 classes.
- Focused on three vehicle categories: `airplane`, `automobile`, `truck`.

---

## Methodology

- **Stable Diffusion** was used as a zero-shot model, guided by engineered text prompts.
- **cDC-GANs** were trained from scratch using one-hot label conditioning.
- Four cDC-GAN configurations were tested per dataset:
  - `adam-bce`, `adam-hinge`, `rmsp-bce`, `rmsp-hinge`
- Evaluation metrics:
  - **Inception Score (IS)**
  - **Fréchet Inception Distance (FID)**
- Planned classifier evaluation (using GAN discriminators) was not completed due to dataset access loss.

---

## Results Summary

### CelebA Results

| Model                  | IS ↑   | FID ↓   |
|-----------------------|--------|---------|
| Stable Diffusion      | 6.85   | 164.50  |
| cDC-GAN (Adam + BCE)  | 5.62   | 198.13  |
| cDC-GAN (Adam + Hinge)| 4.31   | 231.92  |
| cDC-GAN (RMS + BCE)   | 4.89   | 219.34  |

### CIFAR-10 Results

| Model                  | IS ↑   | FID ↓   |
|-----------------------|--------|---------|
| cDC-GAN (Adam + BCE)  | 5.21   | 92.37   |
| cDC-GAN (Adam + Hinge)| 4.38   | 113.28  |
| cDC-GAN (RMS + BCE)   | 4.75   | 107.64  |
| cDC-GAN (RMS + Hinge) | 3.82   | 132.57  |

---

## Key Findings

- **Stable Diffusion** consistently outperformed all cDC-GAN variants in perceptual quality and semantic diversity.
- **Adam + BCE** was the most reliable cDC-GAN setup across both datasets.
- **RMSProp + Hinge** performed the worst, often producing unstable or unrecognizable outputs.
- Conditioning with natural language (Stable Diffusion) offers strong prompt-level control but depends on semantic richness of prompts.
- GANs showed better label controllability and classification utility in structured, low-resolution datasets like CIFAR-10.

---

## Challenges & Limitations

- **Dataset Access:** We lost access to the CelebA dataset midway through experimentation, which prevented us from completing our planned classifier-based evaluation.
- **Training Time:** Each hyperparameter configuration took ~40 minutes to train. This was a significant bottleneck, especially during finals week.
- **Hardware Constraints:** Our experiments were limited by Colab GPU availability and local energy constraints, which restricted the scale of experimentation.
- **Attribute Diversity:** Due to time and data access constraints, we only explored one binary attribute (bangs) in CelebA. Multi-attribute or continuous variable conditioning remains for future work.

---

## Future Work

- Complete the classifier evaluation using repurposed GAN discriminators.
- Extend attribute conditioning in CelebA to include multilabel scenarios.
- Compare with additional generative paradigms (e.g., StyleGAN, VQ-VAE).
- Perform user studies on perceptual realism.

---

## Resources

- Final PDF Report: [`cogs185_project.pdf`](./cogs185_project.pdf)
- Generated Images:
  - [CelebA Samples](https://drive.google.com/drive/u/0/folders/1OefCAcaPU6-Xk801LSuJufcC-z35mKEN)
  - [CIFAR-10 Samples](https://drive.google.com/drive/folders/14NPmN7N3uE2pq3ehhg1wJODlvvt6JuO?usp=sharing)
