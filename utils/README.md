# 🛠️ Utility Functions

This folder contains the backbone for data processing and performance benchmarking.

### `data_utils.py`
- Handles **MedMNIST** data fetching and standardization.
- Implements the **Raster Scan** flattening to convert 2D medical images into 1D sequences for the S4D kernel.

### `logger.py`
- **FLOPs/MACs Counting**: Uses `fvcore` to analyze the computational cost of the model forward pass.
- **VRAM Profiling**: Uses `torch.cuda.max_memory_allocated()` to capture peak memory usage during training.
