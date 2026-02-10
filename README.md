# RAG-PDF AI API 🧠📄

[![Python](https://img.shields.io/badge/python-3.14+-blue)](https://www.python.org/) [![FastAPI](https://img.shields.io/badge/FastAPI-Production-brightgreen)](https://fastapi.tiangolo.com/) [![OpenAI](https://img.shields.io/badge/OpenAI-API-yellowgreen)](https://platform.openai.com/) [![Qdrant](https://img.shields.io/badge/Qdrant-VectorDB-blueviolet)](https://qdrant.tech/)

A **Retrieval-Augmented Generation (RAG)** system for querying PDFs using **OpenAI embeddings**, **Qdrant vector database**, and **FastAPI**.

* Ingest PDFs → chunk & embed automatically
* Ask natural language questions → get AI-generated answers
* FastAPI endpoints with **Swagger docs**

---

## Features ✨

* 📄 PDF ingestion & chunking
* 🧠 RAG query with OpenAI GPT
* 🔍 Qdrant vector search
* 🖥️ Swagger UI documentation (`/docs`)
* Async & scalable with FastAPI + Inngest

---

## Quick Start 🚀

### 1. Clone the repo

```bash
git clone https://github.com/yourusername/rag-pdf-ai.git
cd rag-pdf-ai
```

### 2. Install dependencies

```bash
uv add fastapi uvicorn pydantic python-dotenv qdrant-client inngest openai llama-index
```

### 3. Set environment variables

Create a `.env` file:

```dotenv
OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxxxxxx
QDRANT_URL=http://localhost:6333
```

### 4. Start Qdrant

Run locally:

```bash
docker run -p 6333:6333 qdrant/qdrant
```

### 5. Run the API

```bash
uv run uvicorn main:app --reload
```

* Swagger UI: [http://localhost:8000/docs](http://localhost:8000/docs)
* ReDoc: [http://localhost:8000/redoc](http://localhost:8000/redoc)

---

## API Usage ⚡

### Ingest PDF

**POST `/rag/ingest_pdf`**

```json
{
  "pdf_path": "data/my_document.pdf",
  "source_id": "my-doc-001"
}
```

**Response**

```json
{
  "ingested": 25
}
```

---

### Query PDF

**POST `/rag/query_pdf_ai`**

```json
{
  "question": "What are the service charge rules?",
  "top_k": 5
}
```

**Response**

```json
{
  "answer": "The service charge rules are...",
  "sources": ["my-doc-001"],
  "num_contexts": 5
}
```

---

## Project Structure 🗂️

```
rag-prodapp/
├─ main.py           # RAG workflow + Inngest orchestration
├─ vector_db.py      # Qdrant storage & search
├─ data_loader.py    # PDF loading, chunking, embedding
├─ custom_types.py   # Pydantic models for type safety
├─ .env              # Environment variables
├─ README.md         # Project docs
```

---

## How It Works 🔄

1. **PDF Ingestion:**
   Load PDF → split into chunks → embed → store in Qdrant
2. **Query:**
   Embed user question → search vector DB → retrieve top-k chunks → send to GPT → return answer
3. **Orchestration:**
   `main.py` + Inngest handles async workflow; `data_loader.py` + `vector_db.py` handle logic

---

## Best Practices ✅

* Keep OpenAI API key secret
* Run Qdrant with persistent storage
* Adjust `chunk_size` & `chunk_overlap` for embeddings quality
* Monitor embedding costs for large PDFs

---

## Future Improvements 🚧

* Async Qdrant queries for faster performance
* Hybrid search (vector + keyword)
* Multiple PDF formats (docx, HTML)
* Caching repeated queries
* Docker / cloud deployment

---

## References 📚

* [FastAPI Docs](https://fastapi.tiangolo.com/)
* [Qdrant Docs](https://qdrant.tech/documentation/)
* [OpenAI API Docs](https://platform.openai.com/docs/api-reference)
* [Inngest Python SDK](https://www.inngest.com/docs/python-sdk)

