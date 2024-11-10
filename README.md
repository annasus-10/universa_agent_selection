# Universa Agent Selection

## Overview

This repository contains the code for an **Agent Selection Algorithm** designed for the Universa Network challenge. It uses FAISS and SentenceTransformer models to efficiently select the best-matching agents based on prompt similarity. The project supports two stages: initial retrieval of top candidates using FAISS and refined ranking with a cross-encoder model.

## Table of Contents
- [Overview](#overview)
- [Installation](#installation)
- [Usage](#usage)
- [Code Structure](#code-structure)
- [Additional Information](#additional-information)
- [References](#references)

## Installation

### Dependencies
To set up the environment, clone this repository and install the required dependencies listed in `requirements.txt`:

```bash
git clone https://github.com/annasus-10/agent_selection_universa/tree/master
cd agent_selection_universa
pip install -r requirements.txt
```

This project requires:
- Python 3.x
- FAISS for efficient similarity search
- SentenceTransformer for embedding creation
- transformers library for cross-encoder re-ranking
- ChromaDB for persistent storage

### Directory Setup
Ensure the following directory structure:
```plaintext
agent_selection_universa/
│
├── agents/                       # Folder containing agent JSON files
├── main.py                       # Entry point script
├── embedding_functions/
│   └── base_embedder.py          # Embedding creation module
├── queries.py                    # Contains sample queries
├── requirements.txt              # Python dependencies
└── README.md                     # Project documentation
```

## Usage

### Running the Project
1. **Load Agents:** JSON files in `agents/` are loaded, containing agent descriptions used to create embeddings.
2. **FAISS Index Initialization:** `setup_faiss_index` in `main.py` builds the FAISS index to support efficient similarity retrieval.
3. **Query Processing:** Run queries by executing `main.py`, which selects the best matching agents for a given prompt.
4. **Cross-Encoder Re-Ranking:** The top 3 candidates from FAISS are further refined using a cross-encoder model.

To execute the pipeline, run:
```bash
python main.py
```

## Code Structure

- **`embedding_functions/base_embedder.py`**: Creates embeddings for agent descriptions using SentenceTransformer. Implements similarity calculations.
- **`main.py`**: Main script; loads agents, builds the FAISS index, processes queries, and performs final ranking.
- **`queries.py`**: Contains sample queries for testing.
- **`vector_store/chromadb_store.py`**: Interfaces with ChromaDB, where agent embeddings are stored for persistence.
- **`benchmark.py`**: Used for performance benchmarking and validation.
- **`selection.py`**: Defines the FAISS-based agent selection algorithm.

Each file contains clear docstrings and comments for easy understanding.

## Additional Information

This project uses FAISS for fast similarity matching, followed by re-ranking with a cross-encoder for high accuracy in selecting the best-matching agent. Implementing persistent storage through ChromaDB facilitates scalability, allowing seamless access to pre-computed embeddings.

### Known Issues
- **Path Issues**: Ensure consistent paths in your environment for proper file loading, especially if sharing the project.
- **GPU Acceleration**: If running on a CPU, embedding and re-ranking processes may be slower. Consider using a GPU for improved performance.

## References
- **FAISS Documentation**: [https://faiss.ai](https://faiss.ai)
- **SentenceTransformer Documentation**: [https://www.sbert.net](https://www.sbert.net)
- **Cross-Encoder Documentation**: [https://huggingface.co/cross-encoder/ms-marco-MiniLM-L-6-v2](https://huggingface.co/cross-encoder/ms-marco-MiniLM-L-6-v2)

