# Gemini: Shakespeare Data Preparation (BPE)

## Overview
This directory handles the preparation of the "Tiny Shakespeare" dataset for fine-tuning GPT-2 models using standard BPE (Byte Pair Encoding).

## Main Responsibilities
-   **Data Acquisition:** Downloads the `input.txt` file containing the Shakespeare corpus.
-   **Tokenization:** Uses the standard GPT-2 tokenizer (`tiktoken`) to encode the text.
-   **Output Generation:** Produces `train.bin` and `val.bin` files suitable for training.

## Key Files
-   **`prepare.py`:**
    -   Downloads `input.txt` if not present.
    -   Encodes the text using `tiktoken`.
    -   Splits the data (90% train, 10% val).
    -   Saves the token IDs to binary files.

## Usage
Run the script to prepare the data:

```bash
python data/shakespeare/prepare.py
```

This is typically used for the `finetune_shakespeare.py` configuration.

## Recent Updates (2026-02-03)
-   **Global:** Core training logic in `root/train.py` was updated (warmup LR calculation fix). No specific changes in this directory.
