# 🧠 Local RAG with Ollama, LangChain & React

Sistema **RAG (Retrieval-Augmented Generation)** local que permite subir documentos (PDF, DOCX, TXT), indexarlos en una base vectorial **Chroma**, y realizar consultas semánticas a través de un modelo de lenguaje (**LLM**) servido por **Ollama** o **Azure OpenAI**.  
El frontend está desarrollado en **React + Vite + TailwindCSS**, y el backend en **FastAPI**.

---

## 🚀 Características principales

- 🔍 **Carga e indexado de documentos** (PDF, DOCX, TXT)  
- 🧠 **Búsqueda semántica** mediante embeddings locales de **Ollama** (`mxbai-embed-large`)
- 💬 **Chat contextual** con los documentos indexados  
- 🧩 **Backend** en FastAPI + LangChain + Chroma  
- ⚛️ **Frontend** en React + Vite + TailwindCSS  
- 🐳 **Infraestructura Dockerizada** con `docker-compose`  
- 🌐 **Compatibilidad con Ollama o Azure OpenAI**  

---

## 🗂️ Estructura del proyecto

```
local-rag-ollama-react/
├── backend/
│   ├── main.py
│   ├── requirements.txt
│   ├── chroma_db/
│   ├── data/
│   ├── src/
│   │   ├── extractor.py
│   │   ├── langgraph_nodes.py
│   │   └── settings.py
│   ├── Dockerfile
│   └── .env
├── frontend/
│   ├── src/
│   ├── public/
│   ├── package.json
│   ├── vite.config.js
│   ├── Dockerfile
│   └── .env
├── docker-compose.yml
└── README.md
```

---

## 🧩 Modelos requeridos

El backend usa dos modelos de **Ollama**:

| Propósito | Modelo | Comando |
|----------|--------|---------|
| Embeddings | `mxbai-embed-large` | `ollama pull mxbai-embed-large` |
| LLM Chat | `llama3.1:8b` | `ollama pull llama3.1:8b` |

Si usás Docker:
```bash
docker exec -it ollama ollama pull mxbai-embed-large
docker exec -it ollama ollama pull llama3.1:8b
```

---

## 🐳 Ejecución con Docker Compose

### 1️⃣ Crear los archivos `.env`

#### `backend/.env`
```
DATA_DIR=/app/data
OLLAMA_URL=http://ollama:11434
OLLAMA URL to see the downloaded models=http://localhost:11434/api/tags
EMBED_MODEL=mxbai-embed-large
LLM_MODEL=llama3.1:8b
```

#### `frontend/.env`
```
VITE_API_URL=http://localhost:8000
```

---

### 2️⃣ Levantar los servicios

```bash
docker compose up --build
```

Servicios:
- 🦙 **Ollama** → `localhost:11434`  
- ⚙️ **Backend FastAPI** → `localhost:8000`  
- 💻 **Frontend React** → `localhost:5173`

---

## 🧾 Endpoints principales

| Método | Endpoint | Descripción |
|--------|-----------|-------------|
| `POST` | `/upload` | Sube un documento |
| `POST` | `/index/{doc_id}` | Indexa un documento |
| `GET`  | `/documents` | Lista documentos |
| `DELETE` | `/documents/{doc_id}` | Elimina un documento |
| `POST` | `/query` | Consulta con contexto |

---

## 🧰 Comandos útiles

```bash
docker compose logs -f backend
docker compose down -v
docker exec -it rag_backend bash
```

---

## 📄 Licencia
MIT License.
