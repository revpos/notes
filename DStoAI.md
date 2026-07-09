# From DS, ML to AI Engineer

## Why now?
- #1 Fastest growing job in the market
- $8.48B Enterprise LLM spend in 2025 - roughly doubled
- 2x budgets moved from innovation into core operations

```
                                    API
                                     ^
    Data/Research                    |                  Product/User
    constrained                      |                  constrained
                                     |
                                     |
                  ML Engineer/       |
  ML Researcher/  Data Scientist/    |
  Research-       Research Engineer  |  AI Engineer      Full-stack
  Scientist                          |                   Engineer
<------------------------------------|---------------------------------->
  - training        - inference      | - chains/agents    - product
  - evals           - data           | - tooling & infra  - platform
                                     |
                                     |
                                     v
```


## Why you're well positioned

- **Statistical Thinking**: You already think distributions, test sets and error analysis.
- **Evalutation Mindset**: Evaluation and reliability are the #1 problem in production AI - 
  and evals are applied data science
- **Python fluency**: The entire AI engineering stack runs on the language you already use daily.

Software engineers come from deterministic systems and struggle when LLMs don't behave
like functions. The SWE has to learn a new way of thinking. **You just have to learn new tools.**


## The Roadmap

### Step 1: Close the Software Engineering gap
- Real Python projects : More out of notebooks - modules, imports, classes and 
                         a clean project structure
- Dependencies with UV : Manage packages and virtual environments properly
- Git as a daily driver: Branch, commit, merge, PR
- Production basics    : Testing, debugging, logging and configuration with .env files

> Goal: You can turn a notebook prototype into a small, modular, structured project
that someone else could run.

### Step 2: Learn the LLM-specific layer
- LLM APIs: The entire OpenAI API and Python SDK - auth, requests, structured outputs, tool calling
- Prompt engineering: Fundamentals plus the core building blocks of LLM systems
- Agents from scratch: Build them yourself before reaching for frameworks - learn the 5 levels of AI Agents
- Context Engineering: Understand why agents fail and how to feed them the right information

> Goal: You can design and build production-ready LLM-powered system and explain why each part exists

### Step 3: Build Production-ready AI backends
- **Build** (FastAPI + Pydantic): Build APIs and validate everything
- **Deploy** (Docker + PostgreSQL): Containerize the app and store data into a database
- **Config**: Manage safely with configuration and environment variables
- **MCP Servers**: Understand how they extend your AI applications

> Goal: You can run a small backend locally or in Docker that connects to a database
and exposes clean API routes

### Step 4: Connect AI to your Data with RAG
- **Chunk**: Split documents into pieces
- **Embed**: Turn text into vectors
- **Store**: Vector database like pgvector
- **Retrieve**: Similarity and hybrid search
- **Evalutate**: Retrieval quality and failure cases

> Goal: You can connect your AI system to custom data sources and retrieve relevant context at runtime.

### Step 5: Lean into Evals and Observability
- **Tracing**: Langfuse for inputs, outputs, latents and token costs
- **Evaluations**: Test datasets, LLM-as-a-judge and regression testing
- **Guardrails**: Prompt injection, PII filtering, output validation

This is where your data science background becomes an unfair advantage - evals are applied data science

> Goal: You can quantify performance, catch regressions early and continuously improve
your AI applications

### Step 6: Ship Projects, not tutorials

#### Build 1: 
[**End-to-End Gen AI Project**](https://www.youtube.com/watch?v=qF5il_9IwME)
FastAPI, PostgreSQL, Docker and a real AI pipeline

#### Build 2:
**Full-stack Gen AI project**
FastAPI, React, Supabase

#### Deploy: 
Pick one cloud provider
AWS, Azure, GCP, Hetzner, or DigitalOcean - ship via Docker

#### At Work:
A real project in your company
Real requirements, real users, real production pressure - no job change needed

## Transition
Picking up on AI projects in your company.
Contribute to Open-source projects.
Read and write quality knowledge bases(books, research papers, blogs and articles) that bridge DS and AI gap.
