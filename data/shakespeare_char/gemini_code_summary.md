# Gemini: Shakespeare Data Preparation (Character-Level)

## Overview
This directory prepares the "Tiny Shakespeare" dataset for character-level language modeling. Unlike the other data directories which use BPE, this implementation treats each character as a token.

## Main Responsibilities
-   **Data Acquisition:** Downloads the `input.txt` file.
-   **Vocabulary Creation:** Builds a simple character-to-integer mapping based on the unique characters in the text.
-   **Tokenization:** Encodes the text using this custom character mapping.
-   **Metadata Storage:** Saves the vocabulary (mapping) to `meta.pkl` so the model can decode predictions back to text.

## Key Files
-   **`prepare.py`:**
    -   Builds the vocabulary (`stoi`, `itos`).
    -   Encodes the dataset.
    -   Saves `train.bin`, `val.bin`, and `meta.pkl`.

## Usage
Run the script to prepare the data:

```bash
python data/shakespeare_char/prepare.py
```

This is used for training small, character-level models (e.g., `config/train_shakespeare_char.py`).
