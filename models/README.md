# 🏗️ Model Architectures

This directory contains the core implementations for the architectures evaluated in this research. The project compares a traditional patch-based Transformer approach with a modern State Space Model (SSM) designed for efficient sequence modeling.

## 📂 Folder Structure

| File | Class Name | Description |
| :--- | :--- | :--- |
| `vit_model.py` | `ViT` | Vision Transformer utilizing Global Self-Attention. |
| `s4d_model.py` | `S4DModel` | Diagonal Structured State Space Model (S4D). |

---

## 🔍 Architecture Details

### 1. Vision Transformer (ViT)
The ViT implementation serves as the performance baseline. It processes images by dividing them into fixed-size patches which are then embedded and processed as a sequence.

* **Attention Mechanism**: Global Multi-Head Self-Attention (MSA).
* **Positional Encoding**: Learnable 1D absolute positional embeddings.
* **Scaling**: $O(L^2)$ complexity relative to sequence length.



### 2. Structured State Space (S4D)
The S4D model represents the "Diagonal" variant of Structured State Space models. It is designed to capture long-range dependencies with significantly fewer parameters than Transformers.

* **Core Logic**: Uses a diagonalized transition matrix $\mathbf{\Lambda}$ for efficient computation.
* **Initialization**: Uses the **HiPPO** (High-Order Polynomial Projection Operators) framework for stable memory.
* **Scaling**: $O(L \log L)$ complexity, enabling the processing of long sequences (e.g., $64 \times 64$ flattened pixels) with minimal overhead.



---

## 🛠️ Usage

To use these models in your scripts, you can import them as follows:

```python
from models.vit_model import ViT
from models.s4d_model import S4DModel

# Initialize ViT (e.g., for 64x64 images)
model_vit = ViT(img_size=64, num_classes=11)

# Initialize S4D (e.g., for 64x64 images flattened to 4096)
model_s4d = S4DModel(d_input=1, d_model=256, n_layers=4, n_classes=11)

📊 Comparison at a GlanceFeatureVision Transformer (ViT)Structured State Space (S4D)Parameters~22.14 M~0.20 MComplexityQuadratic $O(L^2)$Linear $O(L \log L)$MemoryEfficient at small resolutionsHigh VRAM at high resolutionsBest ForComplex spatial relationshipsHigh-throughput, resource-constrained
