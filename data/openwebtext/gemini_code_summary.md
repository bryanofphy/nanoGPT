# OpenWebText Data Preparation

## Overview
This directory contains the script to prepare the OpenWebText dataset for training GPT-2 models. OpenWebText is a reproduction of the WebText dataset used by OpenAI to train GPT-2.

## Main Responsibilities
-   **Data Downloading:** Fetches the OpenWebText dataset using the Hugging Face `datasets` library.
-   **Tokenization:** Encodes the text using the GPT-2 BPE (Byte Pair Encoding) via `tiktoken`.
-   **Formatting:** Saves the tokenized data into binary files (`train.bin`, `val.bin`) for efficient memory mapping during training.

## Key Files
-   **`prepare.py`:** The main script.
    -   Downloads the dataset.
    -   Splits it into training and validation sets.
    -   Tokenizes the text using multiple processes for speed.
    -   Writes the output to compressed numpy binary files.

## Usage
Run the preparation script to generate the binary data files:

```bash
python data/openwebtext/prepare.py
```

This will create `train.bin` (~17GB) and `val.bin` (~8.5MB) in this directory.
