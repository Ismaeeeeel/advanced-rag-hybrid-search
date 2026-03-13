# Advanced RAG with Hybrid Search & Reranking 🚀

This repository contains a high-performance Retrieval-Augmented Generation (RAG) pipeline designed for production environments. It addresses common RAG challenges such as retrieval noise and semantic drift by implementing a multi-stage retrieval process.

## 🛠️ Key Features

- **Hybrid Search:** Combines keyword-based (BM25) and semantic (Vector) search for robust retrieval across diverse query types.
- **Two-Stage Retrieval:** Initial retrieval followed by a Cross-Encoder reranking stage to ensure the most relevant context is passed to the LLM.
- **Modular Design:** Easily swap out embedding models, vector databases (Qdrant/Pinecone), or LLM providers.
- **Query Expansion:** Integrated query rewriting to handle complex or ambiguous user intents.

## 🏗️ Architecture

1. **Ingestion:** Documents are chunked using recursive character splitting and indexed in both a BM25 index and a Vector DB.
2. **Retrieval:**
   - Top-K results from BM25.
   - Top-K results from Vector Search.
   - Reciprocal Rank Fusion (RRF) to merge results.
3. **Reranking:** Re-score merged results using a `cross-encoder/ms-marco-MiniLM-L-6-v2` model.
4. **Generation:** Final context + query sent to LLM (GPT-4/Claude-3).

## 🚀 Quick Start

```bash
pip install -r requirements.txt
python main.py --query "How to implement hybrid search?"
```