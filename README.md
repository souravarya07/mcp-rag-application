# 🧠 MCP-RAG Application

An AI-powered FAQ assistant built using Retrieval-Augmented Generation (RAG) powered by [FastMCP](https://github.com/markriedl/fastmcp), [Qdrant](https://qdrant.tech/), [LlamaIndex](https://github.com/jerryjliu/llama_index), and **Ollama running locally**. This app answers Python-related questions using embedded FAQ data and can optionally search the web via [Firecrawl](https://firecrawl.dev/).

---

## 📦 Features

- 🔍 **RAG-enabled FAQ Engine**: Extracts answers from embedded documents.
- 🤖 **Local LLM with Ollama**: Runs large language models like `llama3` without cloud APIs.
- 🧰 **Tool-based Interaction**: Extensible tool system using FastMCP.
- 🔗 **Firecrawl Web Search Tool**: Optional external search for unanswered queries.
- 🧠 **LlamaIndex Embeddings**: Uses HuggingFace models for semantic search.
- ⚡ **FastAPI + Uvicorn**: Lightweight server for local or production use.
- 📥 **Qdrant Vector Store**: Used for high-performance vector-based retrieval.

---

## 🛠️ Tech Stack

| Component        | Description                          |
|------------------|--------------------------------------|
| Python           | Primary language                     |
| Ollama (local)   | Runs `llama3` model locally          |
| FastAPI + Uvicorn| REST server                          |
| FastMCP          | Tool-based AI framework              |
| Qdrant           | Vector storage backend               |
| LlamaIndex       | Embedding + RAG orchestration        |
| Firecrawl        | Optional web search API              |
| dotenv           | Load environment variables           |

---

## 🧑‍💻 Project Structure

```
mcp-rag-application/
│
├── mcp_server.py               # Main server runner
├── rag_app.py                  # FAQEngine and RAG logic
├── .env                        # API keys and config
├── requirements.txt            # Python dependencies
└── mcp/
    └── server/
        └── fastmcp.py          # Custom FastMCP wrapper
```

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/mcp-rag-application.git
cd mcp-rag-application
```

---

### 2. Install & Start Ollama

Install Ollama (if not already):

```bash
https://ollama.com/download
```

Run your model (e.g., `llama3`):

```bash
ollama run llama3
```

> Make sure Ollama is running locally at `http://localhost:11434`.

---

### 3. Create `.env` File

Create a `.env` file in the root directory:

```env
FIRECRAWL_API_KEY=fc-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
OLLAMA_MODEL=llama3
```

---

### 4. Install Dependencies

```bash
pip install -r requirements.txt
```

Make sure the following are in `requirements.txt`:

```txt
fastapi
uvicorn
python-dotenv
llama-index==0.12.52
qdrant-client
requests
```

---

### 5. Start Qdrant (in Docker)

```bash
docker run -p 6333:6333 -p 6334:6334 \
    -v $(pwd)/qdrant_storage:/qdrant/storage \
    qdrant/qdrant
```

---

### 6. Run the MCP-RAG Server

```bash
python mcp_server.py
```

You should see:

```
Starting MCP server at http://127.0.0.1:8080
```

---

## ✅ Health Check

```bash
curl http://127.0.0.1:8080/health
```

Expected:

```json
{ "status": "ok" }
```

---

## 🧠 How it Works

1. `FAQEngine` embeds Python FAQ data into Qdrant using LlamaIndex.
2. When a query is received:
   - FastMCP triggers the relevant tool.
   - The tool performs RAG over vector data.
   - LLM response is generated using **Ollama locally** (e.g., `llama3`).
   - If needed, web fallback via Firecrawl.
3. You get a structured, context-aware response from your local AI system.

---

## 🧪 Tools

- `python_faq_retrieval_tool(query: str)` — Answers Python questions from embedded knowledge.
- `firecrawl_web_search_tool(query: str)` — Gets external results via Firecrawl API.

---

## 📝 Example Query Flow

1. Question received by server.
2. Tool fetches similar FAQ chunks via Qdrant.
3. Passes chunks + question to `llama3` via Ollama.
4. Returns answer to the user.

---

## 📄 License

MIT License — Use freely, modify openly, contribute kindly.

---

## 🙌 Acknowledgements

- [FastMCP](https://github.com/markriedl/fastmcp)
- [Qdrant](https://qdrant.tech/)
- [LlamaIndex](https://llamaindex.ai/)
- [Firecrawl](https://firecrawl.dev/)
- [Ollama](https://ollama.com/)
