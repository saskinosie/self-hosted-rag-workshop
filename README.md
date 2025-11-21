# Weaviate Workshop - Local Edition

A hands-on workshop for learning Weaviate vector database fundamentals using local models. This version runs entirely on your machine using Ollama, eliminating the need for cloud API keys or external services.

## Overview

This workshop teaches core Weaviate concepts through interactive Jupyter notebooks:

- **Lesson 1**: Introduction to Weaviate - data loading and basic queries 
- **Lesson 2**: Working with pre-vectorized data and Wikipedia imports
- **Lesson 3**: Retrieval Augmented Generation (RAG) patterns
- **Lesson 4**: Multi-tenancy and data isolation
- **Lesson 5**: Vector compression techniques (BQ, PQ, RQ, SQ)
- **Lesson 6**: Role-based access control (RBAC)

## System Requirements

- **Operating System**: macOS, Linux, or Windows with WSL2
- **RAM**: 8GB minimum (16GB recommended for smoother performance)
- **Disk Space**: ~5GB free
  - Docker images: ~1GB
  - Ollama models: ~3GB (nomic-embed-text + llama3.2:1b)
  - Python dependencies: ~500MB
  - Workshop data: ~50MB
- **CPU**: Modern multi-core processor (Apple Silicon, Intel, or AMD)

## Prerequisites

- **Docker Desktop** - [Download here](https://docs.docker.com/get-started/get-docker/)
- **Python 3.10+** with pip
- **Homebrew** (macOS/Linux) - For installing Ollama

## Setup Instructions

### 1. Start Weaviate

Make sure Docker is running

```bash
cd _docker
docker-compose up
```

This starts Weaviate 1.32.9 with API-based modules enabled on port 8080.

### 2. Install Ollama

```bash
brew install ollama
ollama serve
```

Keep this terminal running. The Ollama service needs to stay active.

### 3. Pull Required Models

Open a new terminal and pull the embedding model:

```bash
ollama pull nomic-embed-text
```

Then pull a generative model (choose one):

**Option A - Llama 3.2 (Recommended)**
```bash
ollama pull llama3.2:1b
```
- Memory: ~2-3GB RAM
- Parameters: 1 billion
- Better quality responses

**Option B - Qwen 2.5 (Lightweight)**
```bash
ollama pull qwen2.5:0.5b
```
- Memory: ~1GB RAM
- Parameters: 0.5 billion
- Faster, lower quality responses

### 4. Python Environment

Create and activate a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### 5. Configure Environment Variables

Create or update your [.env](./.env) file with:

```bash
WEAVIATE_URL=http://localhost:8080
WEAVIATE_KEY=root-user-key
OPENAI_URL=http://localhost:11434/v1
OPENAI_API_KEY=ollama
```

> **Note**: The `OPENAI_URL` points to your local Ollama instance. Weaviate's OpenAI integrations are compatible with Ollama's API format.

### 6. Verify Installation

Open [1-intro/0-prep-run.ipynb](./1-intro/0-prep-run.ipynb) and run all cells. This validates:
- Weaviate connection
- Ollama models are accessible
- Data vectorization works correctly

### 7. Download Workshop Data

Run [prep-data.ipynb](./prep-data.ipynb) to download the pre-vectorized datasets used in later lessons.

## Workshop Structure

```
weaviate-workshop/
├── 1-intro/                 # Getting started with Weaviate
├── 2-pre-vectorised-data/   # Working with existing embeddings
├── 3-rag/                   # RAG implementation patterns
├── 4-multi-tenancy/         # Multi-tenant architectures
├── 5-vector-compression/    # Compression techniques
├── 6-rbac/                  # Access control
└── _docker/                 # Weaviate deployment config
```

Each lesson includes:
- Interactive notebooks with exercises
- Complete reference implementations in `/complete` subdirectories
- Real-world examples and use cases

## Troubleshooting

**Weaviate won't start**: Ensure Docker is running and ports 8080/50051 are available.

**Ollama connection errors**: Verify `ollama serve` is running and accessible at `http://localhost:11434`.

**Model not found**: Confirm you pulled the models with `ollama list`.

**Out of memory**: Try the smaller qwen2.5:0.5b model or close other applications.

## Next Steps

Start with [1-intro/0-prep-run.ipynb](./1-intro/0-prep-run.ipynb) and work through the lessons sequentially. Each notebook is self-contained with instructions and explanations.




