# S4-vs-VIT-on-Medical-MNIST
This GitHub README provides a professional overview of your comparative study, incorporating the architecture diagrams and dataset samples you provided.

---

# Vision Transformer (ViT) vs. Structured State Space (S4D) for Medical Image Classification

This repository contains the implementation and comparative analysis of **Vision Transformers (ViT)** and **Diagonal Structured State Space Models (S4D)** applied to various medical imaging modalities from the **MedMNIST** collection. We evaluate these architectures based on parameter efficiency, computational complexity (MACs), and hardware utilization (Peak VRAM/Throughput).

## 📊 Datasets: MedMNIST

We evaluate our models on three distinct medical datasets at  and  resolutions. These datasets represent various clinical challenges including CT scans, skin lesions, and histology.
<img width="1479" height="511" alt="Dataset" src="https://github.com/user-attachments/assets/f13e743c-e651-44e9-8bc7-cba3dda504c7" />

*Representative samples from DermaMNIST, OrganAMNIST, and PathMNIST.*

---

## 🏗️ Model Architectures

We compare two fundamentally different approaches to sequence and image modeling:

### 1. Vision Transformer (ViT)

The ViT baseline treats images as a sequence of patches, utilizing a global Multi-Head Self-Attention (MSA) mechanism. While highly effective at capturing long-range dependencies, it carries a significantly larger parameter footprint.

![VIT](https://github.com/user-attachments/assets/f1629a82-9dae-4e60-97a4-0b1bec1f66d2)


### 2. Structured State Space (S4D)

The S4D model treats image data as a discretized 1D signal. By using a diagonal state transition matrix, it achieves extreme parameter efficiency—maintaining a footprint nearly 110x smaller than the ViT baseline in our tests.

![S4](https://github.com/user-attachments/assets/7fc71480-3a3f-4295-88bc-d79699e2ea5c)

---

## 🚀 Key Benchmarks

Our experiments across **OrganAMNIST**, **DermaMNIST**, and **PathMNIST** reveal critical trade-offs:

| Dataset | Model (Res) | Params | Mult-Adds | Peak VRAM | Throughput |
| --- | --- | --- | --- | --- | --- |
| **OrganAMNIST** | S4D (28X28) | **0.20 M** | **103.57 MB** | 703.14 MB | **1766.26 s/s** |
| **OrganAMNIST** | ViT (28X28) | 22.14 M | 122.45 MB | **684.91 MB** | 1126.30 s/s |
| **DermaMNIST** | S4D (28X28) | **0.66 M** | 2.16 GB | 6745.21 MB | 176.13 s/s |
| **DermaMNIST** | ViT (28X28) | 22.32 M | **410.26 MB** | **2318.66 MB** | **235.52 s/s** |

### Key Observations:

* **Parameter Efficiency**: S4D consistently uses  parameters compared to ViT's .
* **Throughput**: S4D excels at lower resolutions (), significantly outperforming ViT in samples per second.
* **Memory Constraints**: S4D exhibits higher **Peak VRAM** usage at  resolutions, indicating a memory bottleneck during internal state management for longer sequences.

---

## 📈 Performance Results

Detailed confusion matrices and training trajectories for each dataset can be found in the `results/` directory.

## DermaMnist Evaluation 

<img width="997" height="413" alt="combined_sharp_derma_horizontal" src="https://github.com/user-attachments/assets/37508e8c-a2e1-4b2e-a1fc-31462a29c524" />


### OrganAMNIST Evaluation ()

---

## 🛠️ Experimental Setup

* **Optimizer**: AdamW (Weight Decay: 0.01)
* **Scheduler**: Cosine Annealing
* **Learning Rate**: 
* **Batch Size**: 64
* **Epochs**: 5

---
