# Gemini: Root Directory Code Summary

## Overview
This directory contains the core implementation of the nanoGPT project, a simple and efficient repository for training and fine-tuning GPT language models. It includes the model architecture definition, the main training loop, and scripts for inference (sampling).

## Main Responsibilities
-   **Model Architecture:** Defines the GPT model structure (Transformer decoder) in PyTorch.
-   **Training:** Orchestrates the training process, including data loading, optimization, logging, and checkpointing. Supports both single-GPU and distributed training (DDP).
-   **Inference:** Provides functionality to generate text from trained models.
-   **Configuration:** Implements a dynamic configuration system to override hyperparameters via command-line arguments or configuration files.

## Key Files

### `model.py`
Contains the complete GPT model definition.
-   **`GPT` Class:** The main model class, composed of a token embedding, position embedding, and a stack of Transformer blocks.
-   **`Block` Class:** Represents a single Transformer block containing LayerNorms, Causal Self-Attention, and an MLP.
-   **`CausalSelfAttention` Class:** Implements multi-head self-attention with a causal mask. It supports PyTorch 2.0's Flash Attention for efficiency.
-   **`GPTConfig` Dataclass:** Defines the model configuration hyperparameters (layers, heads, embedding size, etc.).

### `train.py`
The primary entry point for training models.
-   **Training Loop:** Manages the forward/backward passes, optimizer steps, and learning rate scheduling.
-   **Distributed Training:** Checks for DDP environment variables to enable multi-GPU training.
-   **Data Loading:** Implements a simple data loader using `numpy.memmap` for efficiency with large datasets.
-   **Checkpointing:** Saves model checkpoints based on validation loss or intervals.

### `sample.py`
A script to generate text samples from a trained model.
-   Can load models from local checkpoints or initialize from OpenAI's pretrained GPT-2 weights.
-   Supports conditioning on a prompt (string or file) and adjusting generation parameters like temperature and top-k sampling.

### `configurator.py`
A lightweight configuration helper.
-   Parses command-line arguments and configuration files to override global variables in the target script (e.g., `train.py` or `sample.py`).
-   Allows flexible experimentation without modifying the core scripts.

## Dependencies
-   **PyTorch:** The deep learning framework used for all model components.
-   **NumPy:** Used for efficient data handling (memory mapping).
-   **TikToken:** Used for tokenization (specifically for GPT-2 encodings).
-   **WandB (Optional):** Integration for experiment tracking and logging.

## Usage Examples

**Training a model:**
```bash
python train.py config/train_shakespeare_char.py
```

**Sampling from a trained model:**
```bash
python sample.py --out_dir=out-shakespeare-char
```

**Benchmarking:**
```bash
python bench.py
```

## Recent Updates (2026-02-03)
-   **`train.py` Optimization:** The warmup learning rate calculation was fixed to ensure a non-zero learning rate at iteration 0. The formula changed to `(it + 1) / (warmup_iters + 1)` (previously implicit `it / warmup_iters`). This ensures smoother training initialization.
