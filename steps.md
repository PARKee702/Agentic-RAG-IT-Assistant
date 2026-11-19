# Enterprise IT Support Agentic RAG Copilot
## Project Implementation Steps

1. **`requirements.txt`** — Configure all required Python dependencies, including LangGraph, LangChain, Groq, Hugging Face, Pinecone, Tavily, FastAPI, document loaders, and other supporting libraries.

2. **`.env`** — Configure API keys, Groq model settings, Pinecone index and namespace, Tavily credentials, embedding model, and application environment variables.

3. **`app/core/config.py`** — Implement centralized application configuration using Pydantic Settings to load and manage environment variables.

4. **`data/sample_kb/`** — Store sample company IT knowledge-base documents, including IT handbooks, service desk procedures, password policies, MFA guidelines, and troubleshooting information.

5. **`app/services/ingestion.py`** — Build the document loading and text chunking pipeline supporting PDF, TXT, Markdown, and DOCX files.

6. **`app/rag/vectorstore.py`** — Integrate Hugging Face Sentence Transformer embeddings using `all-MiniLM-L6-v2` (384 dimensions), connect to Pinecone, store document vectors, and configure semantic retrieval.

7. **`app/rag/workflow.py`** — Build the main Agentic RAG workflow using LangGraph, implementing question routing, private knowledge retrieval, evidence grading, Tavily web search fallback, query rewriting, and answer generation.

8. **`app/services/audit.py`** — Implement SQLite-based audit logging to track user questions, answer sources, and agent execution traces.

9. **`app/api/routes.py`** — Develop FastAPI endpoints for AI chat, document ingestion, and application health checks.

10. **`app/main.py`** — Configure the main FastAPI application, register API routes, initialize logging and audit storage, and connect templates and static files.

11. **`templates/index.html`** — Build the main user interface structure for AI chat, document uploads, answer display, source information, and Agent Trace visualization.

12. **`static/css/style.css`** — Design and customize the frontend with a professional enterprise-style dark interface, using black, navy, and blue accent colors.

13. **`static/js/app.js`** — Implement frontend interactions with FastAPI, including chat requests, dynamic answer rendering, source information, agent execution traces, and document upload responses.

14. **`run.py`** — Create the application entry point to launch the FastAPI server using Uvicorn.

15. **Document Ingestion and Knowledge Base Setup** — Upload sample company IT documents through the `/api/ingest` endpoint, process them into chunks, generate embeddings, and store them in the configured Pinecone index.

16. **Testing and Validation** — Test Groq connectivity, local embedding generation, Pinecone integration, private knowledge retrieval, evidence grading, Tavily web search fallback, answer generation, and frontend functionality.

---

## Customized Technology Stack

| Component | Technology |
|---|---|
| Programming Language | Python |
| Backend | FastAPI |
| Agent Orchestration | LangGraph |
| LLM Provider | Groq |
| LLM Model | `openai/gpt-oss-120b` |
| Embedding Provider | Hugging Face |
| Embedding Model | `all-MiniLM-L6-v2` |
| Vector Database | Pinecone |
| External Web Search | Tavily |
| Document Processing | LangChain |
| Text Splitting | RecursiveCharacterTextSplitter |
| Frontend | HTML, CSS, JavaScript |
| Template Engine | Jinja2 |
| Audit Storage | SQLite |

## Project Customization

The original open-source project was customized with:

- Migration from OpenAI API-based LLM inference to Groq.
- Replacement of OpenAI embeddings with local Hugging Face embeddings.
- Updated Pinecone index configuration for 384-dimensional vectors.
- Customized black, navy, and blue frontend design.
- Updated environment configuration and dependency management.
- Updated project documentation and setup instructions.

**Original project:** [Enterprise IT Support Agentic RAG Copilot](https://github.com/entbappy/Enterprise-IT-Support-Agentic-RAG-Copilot)

The original project's license and applicable attribution requirements are respected.