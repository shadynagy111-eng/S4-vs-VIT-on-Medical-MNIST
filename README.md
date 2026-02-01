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

<img width="997" height="413" alt="combined_sharp_horizontal" src="https://github.com/user-attachments/assets/14b1795e-9521-414f-bd4b-ba56bcd5e753" />

## PathMNIST Evaluation ()
<img width="997" height="413" alt="combined_sharp_path_horizontal" src="https://github.com/user-attachments/assets/b52a7ea8-55a0-4cf7-ab63-d5aa5bbcb45e" />


---

## 🛠️ Experimental Setup

* **Optimizer**: AdamW (Weight Decay: 0.01)
* **Scheduler**: Cosine Annealing
* **Learning Rate**: 
* **Batch Size**: 64
* **Epochs**: 5
---
To complete your repository, here is the **"Getting Started"** and **"Repository Structure"** section to follow the previous content. This will help users navigate your code and reproduce your results.

---

## 🛠️ Getting Started

### 1. Prerequisites

Ensure you have Python 3.8+ and a CUDA-capable GPU for performance benchmarking.

```bash
pip install torch torchvision torchaudio medmnist matplotlib numpy

```

### 2. Dataset Preparation

The project utilizes the **MedMNIST v2** library. Datasets are automatically downloaded and preprocessed upon first execution of the training scripts.

* **OrganAMNIST**: Abdominal CT slices.
* **DermaMNIST**: Skin lesion images.
* **PathMNIST**: Histology images.

### 3. Running the Models

To train and evaluate a specific model-resolution pair, use the provided scripts:

```bash
# Example: Train S4D on OrganAMNIST at 64x64
python train.py --model s4d --dataset organmnist --res 64

# Example: Train ViT on PathMNIST at 28x28
python train.py --model vit --dataset pathmnist --res 28

```

---

## 📈 Evaluation Workflow

The evaluation pipeline follows a standardized path from image sequence mapping to final performance metrics.

1. **Image Flattening**: 2D images are converted into 1D sequences via Raster Scan.
2. **Architectural Processing**: Data passes through S4D kernels or Multi-Head Attention blocks.
3. **Metrics Extraction**: Automated logging of MACs (Mult-Adds), VRAM utilization, and classification accuracy.

---

## 📜 Citation

If you use this work or the benchmarks provided, please cite our comparative study:

```bibtex
@article{vit_vs_s4d_medmnist2026,
  title={Comparative Analysis of ViT and S4D in Medical Imaging: Efficiency and Scaling},
  author={Your Name/Research Group},
  year={2026}
}

```

---

