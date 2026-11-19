# Enterprise IT Support Agentic RAG Copilot

An AI-powered IT support assistant that combines **Retrieval-Augmented Generation (RAG), multi-step agent orchestration, semantic search, and web search** to provide context-aware answers to enterprise IT support queries.

The application prioritizes internal company knowledge and uses external web search when private knowledge-base evidence is insufficient.

## Overview

Enterprise IT Support Agentic RAG Copilot is designed to demonstrate how agentic AI and RAG can improve enterprise knowledge retrieval and IT support workflows.

Users can ask IT-related questions in natural language. The system retrieves relevant information from an internal knowledge base, evaluates the retrieved evidence, and generates responses using an LLM.

When internal knowledge is insufficient, the agent can route the query to Tavily Search for external information.

## Key Features

- **Agentic RAG Architecture:** Uses LangGraph to orchestrate the question-answering workflow.
- **Private Knowledge Retrieval:** Retrieves relevant company documents using semantic vector search.
- **Evidence Evaluation:** Grades retrieved knowledge before generating an answer.
- **Intelligent Routing:** Routes questions between private knowledge retrieval and external web search.
- **Web Search Fallback:** Uses Tavily Search when internal evidence is insufficient.
- **Multiple Document Formats:** Supports PDF, TXT, Markdown, and DOCX uploads.
- **Document Processing:** Splits uploaded documents into smaller chunks for efficient retrieval.
- **Vector Embeddings:** Uses a local Hugging Face Sentence Transformer model.
- **Audit Logging:** Records questions, answer sources, and agent traces.
- **Interactive Dashboard:** Provides a custom dark-themed interface for interacting with the AI assistant.
- **Agent Trace Visibility:** Displays routing decisions, retrieval results, evidence grades, and answer sources.

## Architecture

The application follows an agentic RAG workflow built with LangGraph.

### Workflow

1. **Question Input:** The user submits an IT support question.
2. **Question Routing:** The router determines whether the query should be handled using private knowledge.
3. **Knowledge Retrieval:** Pinecone retrieves relevant document chunks using vector similarity search.
4. **Evidence Grading:** The system evaluates whether the retrieved information is relevant.
5. **Web Search Fallback:** If private evidence is insufficient, Tavily Search retrieves external information.
6. **Answer Generation:** Groq generates the final response using the available evidence.
7. **Response Delivery:** The answer, source information, and agent trace are returned to the frontend.

### High-Level Architecture

```text
                User Question
                      |
                      v
               Question Router
                      |
             +--------+--------+
             |                 |
             v                 v
       Private KB          Web Search
        Retrieval            Tavily
             |                 |
             v                 v
       Evidence Grading   Web Evidence
             |              Grading
             v                 |
       Relevant Evidence       |
             |                 |
             +--------+--------+
                      |
                      v
               Answer Generation
                    Groq
                      |
                      v
                Final Response
                      |
                      v
                User Interface
```

## Technology Stack

| Category | Technology |
|---|---|
| Programming Language | Python |
| Backend Framework | FastAPI |
| Agent Orchestration | LangGraph |
| LLM Inference | Groq |
| LLM Model | `openai/gpt-oss-120b` |
| LLM Integration | LangChain Groq |
| Embedding Model | `sentence-transformers/all-MiniLM-L6-v2` |
| Embedding Framework | Hugging Face |
| Vector Database | Pinecone |
| External Search | Tavily Search |
| Document Processing | LangChain Document Loaders |
| Text Splitting | RecursiveCharacterTextSplitter |
| Frontend | HTML, CSS, JavaScript |
| Template Engine | Jinja2 |
| Audit Storage | SQLite |

## RAG Configuration

The current implementation uses the following configuration:

| Component | Configuration |
|---|---|
| Embedding Model | all-MiniLM-L6-v2 |
| Embedding Dimensions | 384 |
| Vector Database | Pinecone |
| Similarity Metric | Cosine |
| Chunk Size | 900 characters |
| Chunk Overlap | 120 characters |
| Retrieval Top-K | 4 |
| LLM Provider | Groq |

The embedding model runs locally, while Pinecone manages vector storage and similarity-based retrieval.

## Project Structure

```text
Enterprise-IT-Support-Agentic-RAG-Copilot/
│
├── app/
│   ├── api/
│   │   └── routes.py
│   │
│   ├── core/
│   │   ├── config.py
│   │   └── logging.py
│   │
│   ├── rag/
│   │   ├── workflow.py
│   │   └── vectorstore.py
│   │
│   ├── services/
│   │   ├── ingestion.py
│   │   └── audit.py
│   │
│   └── main.py
│
├── data/
│   └── sample_kb/
│
├── docs/
├── static/
│   └── css/
│
├── templates/
│   └── index.html
│
├── uploads/
├── requirements.txt
├── run.py
├── Dockerfile
├── .gitignore
└── README.md
```

## Installation and Setup

### 1. Clone the Repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
```

Navigate into the project:

```bash
cd Enterprise-IT-Support-Agentic-RAG-Copilot
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
```

Activate it on Windows:

```cmd
venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create a `.env` file in the project root directory.

Add the following configuration:

```env
GROQ_API_KEY=your_groq_api_key
GROQ_MODEL=openai/gpt-oss-120b

PINECONE_API_KEY=your_pinecone_api_key
PINECONE_INDEX_NAME=fde-it-support-rag-minilm
PINECONE_NAMESPACE=company-it-kb

TAVILY_API_KEY=your_tavily_api_key

EMBEDDING_MODEL=sentence-transformers/all-MiniLM-L6-v2

APP_ENV=development
ADMIN_API_KEY=your_secure_admin_key
```

**Important:** Never commit your `.env` file or expose API keys in your GitHub repository.

### 5. Run the Application

```bash
python run.py
```

The application will be available at:

```text
http://127.0.0.1:8080
```

FastAPI interactive API documentation:

```text
http://127.0.0.1:8080/docs
```

## Document Ingestion

The application supports the following document formats:

- PDF
- TXT
- Markdown (MD)
- DOCX

Documents can be uploaded through the document ingestion API.

**Endpoint:**

```http
POST /api/ingest
```

The ingestion pipeline:

1. Accepts a document upload.
2. Loads the document content.
3. Splits the content into smaller chunks.
4. Generates vector embeddings.
5. Stores the document vectors in Pinecone.

The ingestion endpoint requires the `X-Admin-Key` header.

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/health` | Application health check |
| POST | `/api/chat` | Submit a question to the AI assistant |
| POST | `/api/ingest` | Upload and index documents |
| GET | `/docs` | Interactive API documentation |

## Example Use Cases

- IT account and password support.
- Company VPN troubleshooting.
- Employee access and authentication queries.
- Internal IT policy retrieval.
- Service desk procedures.
- Security-related knowledge retrieval.

## Screenshots

Add your own application screenshots here to demonstrate the customized interface and agent workflow.

Suggested screenshots:

- Main application dashboard.
- Private knowledge-base retrieval.
- Agent Trace showing LangGraph decisions.
- Swagger API documentation.

## Future Improvements

- Add authentication and role-based access control.
- Support larger enterprise document collections.
- Improve document metadata filtering.
- Add conversation memory.
- Implement automated document synchronization.
- Add monitoring and evaluation for retrieval quality.
- Expand support for additional document formats and data sources.

## Learning Outcomes

This project provided hands-on experience with:

- Building agentic AI workflows using LangGraph.
- Implementing Retrieval-Augmented Generation.
- Integrating Groq-hosted language models.
- Generating local semantic embeddings.
- Working with vector databases and Pinecone.
- Building document ingestion pipelines.
- Implementing evidence-based answer generation.
- Integrating external search tools.
- Developing APIs using FastAPI.

## Acknowledgment

This project was developed by customizing and extending the original open-source project:

[Enterprise IT Support Agentic RAG Copilot – Original Repository](https://github.com/entbappy/Enterprise-IT-Support-Agentic-RAG-Copilot)

The current implementation includes modifications to the LLM integration, embedding pipeline, vector database configuration, frontend styling, and project documentation.

Original project licensing and attribution requirements are respected.

---

**Built as a hands-on AI Engineering project focused on Agentic AI, RAG systems, and enterprise knowledge retrieval.**