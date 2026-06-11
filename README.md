# RAG Chunking Strategies Lab

This repository contains a notebook-based lab for comparing chunking strategies in a RAG workflow. It uses two content sources:

- A short podcast-style transcript about trustworthy AI
- A PDF document on trustworthy AI stored in `Document/`

The notebook compares four approaches:

- Fixed-size chunking
- Recursive character chunking
- Token-based chunking
- Semantic chunking, as an advanced optional step

## Repository Layout

- `Notebook/chunking_strategies.ipynb` - main lab notebook
- `Document/` - bundled source files used by the notebook
- `summary.md` - short written conclusion for the lab
- `README.md` - this guide

## What the Notebook Does

The notebook walks through the full chunking workflow:

1. Installs the required packages
2. Loads the transcript and PDF sources
3. Defines helper utilities for token counting and chunk statistics
4. Runs fixed-size, recursive, and token-based chunking
5. Optionally runs semantic chunking if `sentence-transformers` is available
6. Produces charts, summary tables, boundary analysis, and recommendations

The notebook also saves visual outputs such as:

- `chunk_counts.png`
- `token_distributions.png`
- other plots created during the analysis

## Requirements

- Python 3.9 or newer
- Jupyter Notebook or JupyterLab
- Internet access for the first run only if the local PDF is missing

The notebook uses these packages:

- `langchain`
- `langchain-text-splitters`
- `pypdf2`
- `tiktoken`
- `numpy`
- `pandas`
- `matplotlib`

Optional:

- `sentence-transformers` for semantic chunking

## Setup

Install the core dependencies:

```bash
pip install langchain langchain-text-splitters pypdf2 tiktoken numpy pandas matplotlib
```

If you want to use the semantic chunking section, also install:

```bash
pip install sentence-transformers
```

## Run the Lab

1. Open `Notebook/chunking_strategies.ipynb`
2. Run the setup cell
3. Run the notebook from top to bottom

The PDF-loading cell prefers the bundled file in `Document/` first, so the notebook should start quickly even without re-downloading the source.

## Notes

- The podcast transcript is a built-in sample string, so no extra file is needed for that part.
- If the local PDF is not available, the notebook caches a downloaded copy in `.cache/`.
- Semantic chunking is intentionally optional because it is slower and adds an extra dependency.

## Output

When you run the notebook, you get:

- Chunk previews for each strategy
- Chunk-count comparisons
- Token distribution plots
- Broken-sentence analysis
- Final strategy recommendations

## Recommendation

The notebook's final recommendation is:

- For PDF documents, use **Recursive Character Chunking** with `chunk_size=1000` and `chunk_overlap=200`
- For podcast transcripts, use **Token-Based Chunking** with `chunk_size=500` and `chunk_overlap=50`

Why:

- PDFs usually have headings, paragraphs, and section structure that recursive splitting preserves well
- Transcripts usually need token-aware splitting because they are less structured and often feed directly into LLM workflows
- Fixed-size chunking is fast, but it breaks context more often
- Semantic chunking can produce strong results, but it is slower and is best kept as an advanced option

## Recommended Use

Use this lab if you want to understand how chunk size and chunking strategy affect:

- Sentence preservation
- Chunk consistency
- Retrieval readiness for RAG
- Trade-offs between quality and speed
