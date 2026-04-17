Absolutely! Based on project stack (**FastAPI + Docker + Ollama + OpenAI + Postgres + Qdrant + RAG system**), 

---

# RAG Dockerized Service

A **Retrieval-Augmented Generation (RAG) system** built using **FastAPI**, **Ollama**, **OpenAI**, **Postgres**, and **Qdrant**, fully containerized with **Docker**. This system allows uploading documents (PDFs), embedding them into a vector database, and querying using LLMs for accurate retrieval-based responses.

---

## 🔹 Features

* Upload PDFs for document ingestion
* Store vector embeddings in **Qdrant**
* Use **Ollama** or **OpenAI** LLMs for query answering
* Fully containerized using **Docker**
* Multi-client support with customizable embedding and LLM models
* Postgres database for client and metadata management
* Easy local development and deployment

---

## 🔹 Tech Stack

| Component        | Technology                                |
| ---------------- | ----------------------------------------- |
| API              | FastAPI                                   |
| Vector DB        | Qdrant                                    |
| LLM              | Ollama / OpenAI                           |
| Relational DB    | PostgreSQL                                |
| Containerization | Docker                                    |
| Embeddings       | Sentence Transformers / OpenAI embeddings |

---

## 🔹 Project Structure

```
rag_service

---

## 🔹 Setup & Run

### 1️⃣ Clone the repository

```bash
git clone https://github.com/username/repo-name.git
cd repo-name
```

### 2️⃣ Set environment variables

Create a `.env` file in the root:

```env
POSTGRES_USER=postgres
POSTGRES_PASSWORD=yourpassword
POSTGRES_DB=rag_service
POSTGRES_HOST=postgres
POSTGRES_PORT=5432

QDRANT_API_KEY=your-qdrant-api-key
LLM_QWEN=qwen2.5vl:7b
LLM_OPENAI=gpt-4o-mini
OPENAI_API_KEY=your-openai-key
LLM_HOST=ollama
LLM_PORT=11434
```

### 3️⃣ Start all services with Docker

```bash
docker-compose up -d
```

* **Postgres**: Stores clients and metadata
* **Qdrant**: Stores vector embeddings
* **Ollama**: LLM server
* **FastAPI API**: Serves endpoints for ingestion and querying

---

## 🔹 API Endpoints

| Endpoint             | Method | Description                               |
| -------------------- | ------ | ----------------------------------------- |
| `/health`            | GET    | Health check                              |
| `/set_models`        | POST   | Set embedding and LLM models for a client |
| `/update_set_models` | POST   | Update client’s model settings            |
| `/ingest_file`       | POST   | Upload and ingest a PDF file              |
| `/query`             | POST   | Query ingested documents using LLM        |

---

## 🔹 Example Usage

### Upload a PDF

```bash
curl -X POST "http://localhost:8000/ingest_file?client_id=client1&document_id=doc1" \
  -F "file=@./data/pdfs/sample.pdf"
```

### Query the documents

```bash
curl -X POST "http://localhost:8000/query" \
  -H "Content-Type: application/json" \
  -d '{"client_id": "client1", "query": "Explain the fund performance"}'
```

---

## 🔹 Notes

* Ollama models can be pre-pulled or downloaded automatically during first run
* Qdrant stores persistent embeddings in a Docker volume (`qdrant_data`)
* Supports both **Ollama** and **OpenAI** as LLM backends
* Multi-client setup is supported via client-specific embedding and LLM settings

---

## 🔹 License

MIT License © 2025 Gowtham

---


