# RAG Journey

A hands-on set of Jupyter notebooks for learning retrieval-augmented generation (RAG) with LangChain. The notebooks build from preparing text and PDF documents through embedding, vector storage, and querying with hosted or local language models.

## Requirements

- Python 3.13 or later
- [uv](https://docs.astral.sh/uv/) for installing the project dependencies
- A Groq API key for notebooks 1–3
- Docker Desktop with Docker Model Runner enabled for notebook 4

## Setup

From the repository root, install the dependencies:

```powershell
uv sync
```

For notebooks 1–3, copy `.env.example` to `.env` and add your Groq API key:

```dotenv
GROQ_API_KEY=your_api_key
```

Keep the key private; `.env` is excluded from Git. Notebook 4 uses a local model through Docker Model Runner and does not require a Groq API key.

Open a notebook in VS Code or Jupyter and select the Python environment created by `uv` as its kernel.

## Notebooks

| Notebook | What it covers |
| --- | --- |
| [1.1_RAG_With_Own_Text.ipynb](Notebooks/1.1_RAG_With_Own_Text.ipynb) | Prepare your own text, split it into chunks, create embeddings, store them in a vector database, and use the retrieved context. |
| [2.0_RAG_With_PDF.ipynb](Notebooks/2.0_RAG_With_PDF.ipynb) | Apply the same RAG workflow to PDF documents. |
| [3.0_RAG_Local_Persist.ipynb](Notebooks/3.0_RAG_Local_Persist.ipynb) | Reuse a locally persisted vector database and add or query PDF embeddings. |
| [4.0_Docker_Model_Runner.ipynb](Notebooks/4.0_Docker_Model_Runner.ipynb) | Call a local model through Docker Model Runner’s OpenAI-compatible API using LangChain’s `ChatOpenAI` client. |

Sample PDFs are in [`Data/`](Data/). The first three notebooks use Groq for chat completions; the fourth sends a prompt to the local model configured in Docker Model Runner.

## Docker Model Runner

Before running notebook 4:

1. Enable Docker Model Runner in Docker Desktop and make a model available to it.
2. Confirm the model is accessible through the host endpoint used by the notebook: `http://localhost:12434/engines/llama.cpp/v1`.
3. Ensure the model name in the notebook (`ai/laya:latest`) matches a model available in your Docker Model Runner setup.

The notebook passes `api_key="not-needed"` because the request is sent to the local endpoint. If the runner reports a tensor-dimension or model-loading error, the selected model bundle may not be compatible with its current backend; try a compatible model or update Docker Desktop.
