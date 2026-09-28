# ASEEL (أصيل) – Agentic AI System for Saudi Cultural Guidance

ASEEL is an agentic AI system that provides accurate, context-aware guidance on Saudi culture, including customs, etiquette, traditions, and regional diversity. It combines a multi-agent workflow, retrieval-augmented generation (RAG), conversational memory, and translation support, and is exposed through a REST API with a web frontend.

---

## Features

- **Agentic workflow**: specialized agents orchestrated with LangGraph to plan, retrieve, reason, and respond.
- **Retrieval-Augmented Generation**: grounded answers from a curated cultural knowledge base stored in ChromaDB.
- **Multilingual support**: translation layer for Arabic and English interactions.
- **Conversation memory**: keeps context across turns for natural follow-up questions.
- **Regional awareness**: GeoJSON data for Saudi administrative regions, enabling region-specific guidance.
- **Tool use**: pluggable tools the agents can call (lookup, region resolution, quiz/MCQ generation, etc.).
- **Evaluation**: automated quality testing with DeepEval.
- **REST API + Frontend**: FastAPI backend and a dedicated web UI (`aseel-frontend`).
- **Docker-ready**: containerized for easy deployment.

---

## Architecture

```
User ──► Frontend (aseel-frontend)
              │
              ▼
        FastAPI (api/)
              │
              ▼
   LangGraph Workflow (workflow/)
     ├── Agents (agents/)        ← reasoning & task routing
     ├── Tools (tools/)          ← callable capabilities
     ├── Retrieval (retrieval/)  ← ChromaDB + sentence-transformers
     ├── Memory (memory/)        ← conversation state
     └── Translation (translation/)
              │
              ▼
        LLM (OpenAI via LangChain)
```

---

## Project Structure

| Path | Description |
|------|-------------|
| `agents/` | Agent definitions and behavior |
| `api/` | FastAPI application and endpoints |
| `aseel-frontend/` | Web frontend |
| `config/` | Application configuration |
| `data/` | Cultural knowledge base and source data |
| `evaluation/` | Evaluation pipelines and datasets |
| `memory/` | Conversation memory management |
| `prompts/` | Prompt templates |
| `retrieval/` | Embedding, indexing, and vector search (ChromaDB) |
| `scripts/` | Utility and data-preparation scripts |
| `tests/` | Automated tests |
| `tools/` | Tools available to agents |
| `translation/` | Translation utilities |
| `utils/` | Shared helpers |
| `workflow/` | LangGraph workflow / graph definition |
| `regions.geojson` | Saudi administrative regions geodata |
| `Dockerfile` | Container build file |
| `requirements.txt` | Python dependencies |

---

## Tech Stack

- **Language**: Python
- **API**: FastAPI, Uvicorn
- **Agent orchestration**: LangChain, LangGraph
- **LLM**: OpenAI (via `langchain-openai`)
- **Vector store**: ChromaDB
- **Embeddings**: sentence-transformers
- **Data**: pandas, GeoJSON
- **Validation**: Pydantic
- **Evaluation**: DeepEval, pytest
- **Deployment**: Docker

---

## Getting Started

### Prerequisites

- Python 3.10+
- An OpenAI API key
- Node.js 18+ (for the frontend)
- Docker (optional)

### 1. Clone the repository

```bash
git clone https://github.com/fatimacoding/ASEEL-Agentic-AI.git
cd ASEEL-Agentic-AI
```

### 2. Set up the backend

```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### 3. Configure environment variables

Create a `.env` file in the project root:

```env
OPENAI_API_KEY=your_api_key_here
```

### 4. Build the knowledge base

Index the cultural data into ChromaDB using the scripts in `scripts/`:

```bash
python scripts/<ingestion_script>.py
```

### 5. Run the API

```bash
uvicorn api.main:app --reload
```

The API will be available at `http://localhost:8000`, with interactive docs at `http://localhost:8000/docs`.

### 6. Run the frontend

```bash
cd aseel-frontend
npm install
npm run dev
```

> Adjust the script names and module paths above to match your actual entry points.

---

## Docker

```bash
docker build -t aseel .
docker run -p 8000:8000 --env-file .env aseel
```

---

## Testing & Evaluation

Run the test suite:

```bash
pytest tests/
```

Run the evaluation pipeline (DeepEval):

```bash
python -m evaluation.<evaluation_script>
```

---

## Example Questions

- "What is the proper etiquette when visiting a Saudi home?"
- "How is Arabic coffee traditionally served?"
- "What are the customs of the Hejaz region?"
- "ما هي عادات الضيافة في نجد؟"

---

## Roadmap

- [ ] Expand the cultural knowledge base across all regions
- [ ] Add voice input and output
- [ ] Improve Arabic dialect understanding
- [ ] Add more evaluation benchmarks
---

