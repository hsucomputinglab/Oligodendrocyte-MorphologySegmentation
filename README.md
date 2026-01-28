# AI-Based Morphological Segmentation of Oligodendrocyte Myelin Plasticity

> **⚠️ Note:** This repository contains the demonstration and performance benchmarks for a deep learning pipeline currently under review for publication. The full source code and trained weights will be released upon acceptance.

## 🔬 Project Overview

Quantifying oligodendrocyte (OL) morphology in high-throughput screens is a significant challenge due to the intricate, recursive branching of mature myelin sheaths. Traditional tools often rely on qualitative descriptors or convex shape assumptions (e.g., Cellpose [1]) or are designed for tubular structures (e.g., AxonDeepSeg [2]), failing to capture the "broken branch" topology of complex arbors.

This project introduces a minimal, auditable deep learning pipeline designed to convert pixel-level segmentations of whole-well MBP (Myelin Basic Protein) images into rigorous, well-level statistical endpoints.

**Key Capabilities:**
* **Granular Segmentation:** Distinguishes between **Membranous (sheaths)**, **Non-membranous (soma)**, and **Cell Debris**.
* **Topology-Aware Architecture:** Utilizes a modified U-Net [3] backbone augmented with spatial-channel squeeze-excitation (scSE) [4] and a Vision Transformer (ViT) bottleneck [5] to preserve fine branching structures.
* **Automated Quantification:** Aggregates object-level metrics to reveal biological maturation trends, specifically differentiating between sheath expansion and simple cell proliferation.

---

## 🖥️ Application Demo

We have developed a GUI to facilitate the batch processing of high-content screening data. The application visualizes the segmentation mask and provides real-time quantification of component counts and areas.

### **[▶️ Click here to watch the Application Demo](ApplicationDemo.mp4)**
*(Clicking the link above will open the video player in a new window)*

---

## 📊 Performance Benchmarks

We benchmarked our proposed architectures (**scSE-Modified** and **ViT-Modified**) against standard baselines (Plain ConvUNet [3]) and state-of-the-art state-space models (U-Mamba [6]).

Our **ViT-Modified** variant achieves the highest structural fidelity, particularly for the challenging "Membranous" class, while maintaining reasonable computational efficiency.

| Model | Params (M) | Size (MB) | FLOPs (G) | Dice (%) | IoU (%) | Train (s/ep) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Plain ConvUNet** [3] | 7.77 | 62.2 | 48.42 | 76.93 | 65.58 | 22 |
| **UMambaBot** [6] | 17.15 | 90.2 | 96.43 | 80.34 | 69.81 | 69 |
| **UMamba Enc** [6] | 11.38 | 91.3 | 94.56 | 81.21 | 70.47 | 98 |
| **scSE-Modified (Ours)** | 23.18 | 185.7 | 65.25 | 83.48 | 74.29 | 56 |
| **ViT-Modified (Ours)** | **39.76** | **318.3** | **66.32** | **89.43** | **83.77** | **57** |

*Table 1: Performance vs. Complexity comparison. The ViT-Modified architecture achieves a Dice score of 89.43% and IoU of 83.77% on held-out tiles.*

---

## 📅 Availability

The full source code, including the model architecture definitions, training scripts, and the quantification GUI, will be made available here following the publication of the associated manuscript.

**Contact:**
For questions regarding the dataset or methodology prior to publication, please reach out to the corresponding author.

---

## 📚 References

[1] Stringer, C., et al. (2020). Cellpose: a generalist algorithm for cellular segmentation. *Nature Methods*, 18(1):100-106.

[2] Zaimi, A., et al. (2017). AxonDeepSeg: Automatic axon and myelin segmentation from microscopy data using convolutional neural networks. *arXiv preprint arXiv:1711.01004*.

[3] Ronneberger, O., et al. (2015). U-Net: Convolutional networks for biomedical image segmentation. *MICCAI*, 234-241.

[4] Roy, A. G., et al. (2018). Concurrent spatial and channel 'squeeze & excitation' in fully convolutional networks. *arXiv preprint arXiv:1803.02579*.

[5] Chen, J., et al. (2021). TransUNet: Transformers make strong encoders for medical image segmentation. *arXiv preprint arXiv:2102.04306*.

[6] Ma, J., et al. (2024). U-Mamba: Enhancing long-range dependency for biomedical image segmentation. *arXiv preprint arXiv:2401.04722*.