# S4-vs-VIT-on-Medical-MNIST
# S4 vs ViT on Medical-MNIST

Repository for experiments comparing S4-based models and Vision Transformers on Medical-MNIST.

Contents
- `src/` — code: data loaders, model wrappers, training and evaluation scripts
- `configs/` — experiment configuration files (YAML)
- `experiments/` — run scripts and results
- `notebooks/` — exploratory analysis and visualizations
- `checkpoints/`, `logs/` — saved models and training logs

Quick start
1. Create a virtual environment and install requirements:
   ```
   python -m venv .venv
   source .venv/bin/activate
   pip install -r requirements.txt
   ```

2. Prepare dataset (example uses MedMNIST):
   - See `src/data/dataloader.py` for automated download using the `medmnist` package.

3. Run training (example):
   ```
   python src/train.py --config configs/default.yaml --model vit
   # or
   python src/train.py --config configs/default.yaml --model s4
   ```

4. Evaluate:
   ```
   python src/evaluate.py --checkpoint checkpoints/best.pth --model vit
   ```

Notes
- ViT is implemented via the `timm` package. S4 requires an external implementation — see `src/models/s4_wrapper.py` for integration instructions.
- Logging: TensorBoard and optional W&B integration (toggle in config).
