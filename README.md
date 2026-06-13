# LAB | Relevance Scoring and Rerankers

This repository contains a notebook-based lab for improving RAG retrieval with:

- Metadata filtering
- Baseline embedding retrieval
- LLM-based relevance scoring
- Cohere reranking

The lab uses two bundled sources in `Document/`:

- A PDF on trustworthy AI
- A podcast-style audio file about trustworthy AI

## Repository Layout

- `Notebook/relevance_scoring_rerankers.ipynb` - main lab notebook
- `Document/` - bundled PDF and audio sources used by the notebook
- `lab_summary.md` - short written conclusion for the lab
- `README.md` - this guide

## What The Notebook Does

The notebook walks through an end-to-end relevance-ranking workflow:

1. Installs the required packages
2. Loads API keys and initializes OpenAI and Cohere clients
3. Loads the PDF and transcribes the podcast with Whisper
4. Chunks both sources and attaches rich metadata
5. Builds embeddings and runs baseline similarity search
6. Applies optional LLM scoring and Cohere reranking
7. Filters results by metadata such as `source_type`
8. Runs a full RAG pipeline and compares retrieval quality

The notebook also prints sample answers and score comparisons so you can manually judge whether reranking improves relevance.

## Requirements

- Python 3.9 or newer
- Jupyter Notebook or JupyterLab
- API access for OpenAI
- Optional: Cohere API key for the reranking step

The notebook uses these packages:

- `openai`
- `numpy`
- `pypdf2`
- `tiktoken`
- `python-dotenv`
- `cohere`
- `sentence-transformers`
- `pydub`
- `imageio[ffmpeg]`
- `openai-whisper`

## Setup

Install the core dependencies:

```bash
pip install openai numpy pypdf2 tiktoken python-dotenv pydub imageio[ffmpeg] openai-whisper
```

If you want to use the Cohere reranker and semantic tooling, also install:

```bash
pip install cohere sentence-transformers
```

## Configure API Keys

Set your keys in a `.env` file or in your environment:

```bash
OPENAI_API_KEY=your_key_here
COHERE_API_KEY=your_key_here
```

The Cohere key is optional, but the notebook expects OpenAI access for embeddings, scoring, and Whisper transcription.

## Run The Lab

1. Open `Notebook/relevance_scoring_rerankers.ipynb`
2. Run the dependency installation cell
3. Load the API keys and initialize the clients
4. Run the notebook from top to bottom

The notebook first tries to use the bundled files in `Document/`, so it can run without downloading new source content.

## Notes

- The PDF and audio file are both part of the repo, which keeps the lab self-contained.
- Whisper transcription may take a little time on the first run.
- Cohere reranking is optional; the notebook still works with baseline retrieval and LLM scoring if the Cohere key is missing.
- Metadata filtering is useful when you want to query only the PDF or only the podcast transcript.

## Output

When you run the notebook, you get:

- Sample retrieval answers for each strategy
- Baseline, LLM, and Cohere score comparisons
- Metadata-filtered retrieval examples
- A full RAG pipeline that can switch rerankers with one argument
- A final manual evaluation prompt for comparing result quality

## Recommendation

The lab's recommendation is to choose the retrieval strategy by source type:

- For the PDF, use recursive chunking with rich metadata and baseline or reranked retrieval
- For the podcast transcript, use the same metadata-aware pipeline, then compare baseline retrieval against LLM or Cohere reranking
- Use Cohere reranking when you want the strongest relevance ordering and can afford the extra API call
- Use baseline retrieval when you want the simplest and fastest option

Overall, the lab shows that metadata filtering plus reranking is more flexible than plain similarity search, especially when the same query needs to behave differently across PDF and audio-derived text.
