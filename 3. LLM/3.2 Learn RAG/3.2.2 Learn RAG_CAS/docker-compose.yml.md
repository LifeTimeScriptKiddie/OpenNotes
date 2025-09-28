# **🐳 Docker Compose Overview**

  

Sets up a 3-service architecture for a local RAG pipeline:

- Ollama for local LLM inference and embedding
    
- Open WebUI for document management
    
- rag-backend for backend processing, embedding, and automation
    

---

## **Service Breakdown**

  

###  **ollama**

|**Config**|**Description**|
|---|---|
|image|ollama/ollama (official image)|
|ports|Exposes 11434 for LLM/embedding API|
|volumes|Persists Ollama model cache|
|restart|Automatically restarts unless stopped manually|

```
ollama:
  image: ollama/ollama
  ports:
    - "11434:11434"
  volumes:
    - ollama_data:/root/.ollama
  restart: unless-stopped
```

---

### **open-webui**

|**Config**|**Description**|
|---|---|
|image|WebUI UI/API interface|
|ports|UI served at http://localhost:3000|
|environment|Points to Ollama endpoint (host.docker.internal)|
|volumes|Persists uploaded documents and app data|
|extra_hosts|Maps host.docker.internal to host IP|

```
open-webui:
  image: ghcr.io/open-webui/open-webui:main
  ports:
    - "3000:8080"
  environment:
    - OLLAMA_BASE_URL=http://host.docker.internal:11434
  volumes:
    - openwebui_data:/app/backend/data
  extra_hosts:
    - host.docker.internal:host-gateway
  restart: unless-stopped
```

---

### **rag-backend**

|**Config**|**Description**|
|---|---|
|build|Built from ./rag_backend directory|
|depends_on|Starts after ollama and open-webui|
|volumes|Mounts local source code for hot reload|
|env_file|Loads .env variables (embedding/backend config)|
|command|Runs cron in foreground for scheduled uploads|
|extra_hosts|Enables container-to-host networking|

```
rag-backend:
  build: ./rag_backend
  depends_on:
    - ollama
    - open-webui
  volumes:
    - ./rag_backend:/app
  env_file:
    - ./rag_backend/.env
  extra_hosts:
    - host.docker.internal:host-gateway
  restart: unless-stopped
  command: cron -f
```

---

## **Named Volumes**

|**Volume**|**Purpose**|
|---|---|
|ollama_data|Caches downloaded Ollama models|
|openwebui_data|Stores WebUI data and uploads|

```
volumes:
  openwebui_data:
  ollama_data:
```
ㄴ