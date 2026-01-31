# Gemini: Config Directory Code Summary

## Overview
This directory contains configuration files used to customize the training and evaluation of nanoGPT models. These files are Python scripts that define specific hyperparameter overrides.

## Main Responsibilities
-   **Hyperparameter Management:** Provides presets for different training scenarios, such as pre-training large models or fine-tuning on smaller datasets.
-   **Experiment Definition:** Defines specific experiments (e.g., "Train GPT-2 124M on OpenWebText") by grouping relevant parameters like batch size, learning rate, and model dimensions.

## Key Files & Roles
The files in this directory are meant to be passed as arguments to `train.py` (or other scripts using `configurator.py`). They typically override global variables defined in the main script.

-   **`train_gpt2.py`:** Configuration for reproducing GPT-2 (124M) training on the OpenWebText dataset. It sets parameters for a large-scale distributed run (e.g., `batch_size`, `gradient_accumulation_steps`, `max_iters`).
-   **`finetune_shakespeare.py`:** Configuration for fine-tuning a pretrained GPT-2 XL model on the Shakespeare dataset. It adjusts parameters for fine-tuning (e.g., lower learning rate, `init_from='gpt2-xl'`).
-   **`eval_*.py`:** (Inferred) Configurations specifically tuned for model evaluation or benchmarking.

## Mechanism
These files work in conjunction with `configurator.py` in the root directory. When `train.py` is executed with a config file argument, the content of the config file is executed, updating the global namespace of the training script with the defined values.

## Usage Example

To train a GPT-2 model using the specific configuration in `train_gpt2.py`:

```bash
python train.py config/train_gpt2.py
```

To fine-tune on Shakespeare:

```bash
python train.py config/finetune_shakespeare.py
```
