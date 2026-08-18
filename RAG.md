# RAG Project Structure

```text
 .
├──  .git
├──  logs                        # Log files for debugging and monitoring
│   └──  app.log
├── 󰣞 src
│   ├──  api                     # API endpoints (Fast API/Flask)
│   │   ├──  __init__.py
│   │   └──  routes.py
│   ├──  chunking                # Split text into small chunks
│   │   ├──  __init__.py
│   │   └──  chunker.py
│   ├──  embeddings              # Convert text chunks into embeddings
│   │   ├──  __init__.py
│   │   └──  embedder.py
│   ├──  ingestion               # Load data from PDFs, CSVs. websites, etc
│   │   ├──  __init__.py
│   │   └──  loader.py
│   ├──  llm                     # Handle LLM calls (OpenAI, Claude, Gemini, etc)
│   │   ├──  __init__.py
│   │   └──  llm_client.py
│   ├──  prompts                 # Store prompt templates
│   │   ├──  __init__.py
│   │   └──  prompt_templates.py
│   ├──  retrieval               # Retrieve relevant chunks using similarity search
│   │   ├──  __init__.py
│   │   └──  retriever.py
│   ├──  utils                   # Helper functions and common utilities
│   │   ├──  __init__.py
│   │   └──  helpers.py
│   └──  vectordb                # Handle vector db operations(ChromaDB/Pinecone/FAISS)
│       ├──  __init__.py
│       └──  vector_store.py
├──  tests                       # Unit & Integration Tests suite
│   └──  test_app.py
├──  .env                        # Environment(Secret) Variables
├── 󰊢 .gitignore                  # Tells Git what files/folders to ignore
├──  .python-version             # Pin python version
├──  config.yaml                 # Config for models, chunk size, DB settings
├──  main.py                     # Entry point of the application
├──  pyproject.toml              # Project config with UV
├── 󰂺 README.md                   # Project Structure, setup guides, HOWTOs, Architecture
└──  requirements.txt            # List of all Python dependencies
```
