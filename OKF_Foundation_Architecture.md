# Open Knowledge Format (OKF) -- Foundational Architecture

> **Core Principle:**\
> Knowledge should be **human-readable, machine-readable,
> version-controlled, and AI-consumable.**

------------------------------------------------------------------------

# High-Level Architecture

``` text
                         ┌─────────────────────────┐
                         │     User / AI Agent     │
                         └───────────┬─────────────┘
                                     │
                    Query / Search / Edit / Generate
                                     │
                         ┌───────────▼─────────────┐
                         │   Knowledge API Layer   │
                         │ REST │ GraphQL │ MCP    │
                         └───────────┬─────────────┘
                                     │
         ┌───────────────────────────┼────────────────────────────┐
         │                           │                            │
         ▼                           ▼                            ▼
 ┌─────────────────┐       ┌──────────────────┐        ┌─────────────────┐
 │ Search Engine   │       │ Knowledge Graph  │        │ AI Services     │
 │ BM25 + Vector   │       │ Relations        │        │ LLM/RAG/Agents  │
 └────────┬────────┘       └────────┬─────────┘        └────────┬────────┘
          │                         │                           │
          └──────────────┬──────────┴──────────────┬────────────┘
                         ▼                         ▼
              ┌──────────────────────────────────────────┐
              │         Knowledge Repository             │
              │                                          │
              │ Markdown │ YAML │ JSON │ Images │ PDFs   │
              │ Version Controlled (Git)                 │
              └───────────────┬──────────────────────────┘
                              │
          ┌───────────────────┼────────────────────┐
          ▼                   ▼                    ▼
 ┌────────────────┐  ┌──────────────────┐  ┌─────────────────┐
 │ Metadata Layer │  │ Ontology Layer   │  │ Asset Registry  │
 │ tags           │  │ entities         │  │ files           │
 │ authors        │  │ taxonomy         │  │ datasets        │
 │ timestamps     │  │ relationships    │  │ APIs            │
 └────────────────┘  └──────────────────┘  └─────────────────┘
```

------------------------------------------------------------------------

# 1. Knowledge Layer (Source of Truth)

Everything is stored as plain files.

``` text
knowledge/
│
├── concepts/
├── projects/
├── datasets/
├── apis/
├── models/
├── prompts/
├── experiments/
├── tutorials/
├── decisions/
├── people/
└── assets/
```

Each knowledge object is independent.

Example:

``` text
concepts/
    rag.md

projects/
    hiring-assistant.md

datasets/
    imdb.md
```

------------------------------------------------------------------------

# 2. Metadata Layer

Every document starts with structured metadata.

``` yaml
---
id: rag-001
title: Retrieval Augmented Generation
type: concept

tags:
  - llm
  - retrieval

author: Ashwani

created: 2026-07-05
updated: 2026-07-05

status: stable

related:
  - vector-db
  - embeddings
---
```

Benefits:

-   Standardized metadata
-   Easy indexing
-   Filtering
-   Automation
-   Validation

------------------------------------------------------------------------

# 3. Knowledge Content Layer

``` markdown
# Retrieval Augmented Generation

## Definition

...

## Workflow

...

## Advantages

...

## Limitations

...
```

The content remains readable for humans while remaining structured
enough for machines.

------------------------------------------------------------------------

# 4. Semantic Layer

Knowledge objects are connected as a graph.

``` text
RAG
 ├── uses → Embeddings
 ├── uses → Vector DB
 ├── extends → Search
 └── related → LangChain
```

Relationship metadata:

``` yaml
relations:

uses:
  - embeddings
  - qdrant

extends:
  - semantic-search
```

------------------------------------------------------------------------

# 5. Indexing Layer

``` text
Markdown
      │
      ▼
Parser
      │
      ├── Full Text Index
      ├── Metadata Index
      ├── Tag Index
      ├── Embedding Index
      └── Graph Index
```

Supports:

-   Keyword Search
-   Semantic Search
-   Hybrid Search
-   Graph Traversal

------------------------------------------------------------------------

# 6. AI Layer

``` text
Question
   │
   ▼
Search
   │
   ▼
Relevant Documents
   │
   ▼
Context Builder
   │
   ▼
LLM
   │
   ▼
Answer
```

Possible extensions:

-   Chunk ranking
-   Reranking
-   Source attribution
-   Citations
-   Long-term memory
-   Agent workflows

------------------------------------------------------------------------

# 7. API Layer

``` http
GET /documents
GET /concepts
GET /search?q=rag
GET /graph/rag

POST /ingest
POST /chat
```

Can expose:

-   REST API
-   GraphQL
-   MCP Server
-   WebSocket events

------------------------------------------------------------------------

# 8. Version Control Layer

Git acts as the persistence layer.

Benefits:

-   Version history
-   Collaboration
-   Branching
-   Rollback
-   Pull requests
-   Audit trail

------------------------------------------------------------------------

# Recommended Folder Structure

``` text
knowledge-base/

├── concepts/
├── projects/
├── datasets/
├── models/
├── prompts/
├── decisions/
├── notes/
├── tutorials/
├── people/
├── assets/
│
├── ontology/
│   ├── taxonomy.yaml
│   ├── schema.yaml
│   └── relations.yaml
│
├── index/
│   ├── embeddings/
│   ├── vectors/
│   ├── graph/
│   └── search/
│
├── api/
├── config/
└── README.md
```

------------------------------------------------------------------------

# Design Principles

-   Plain text first
-   Human-readable and machine-readable
-   Git-native
-   AI-native
-   Extensible
-   Searchable
-   Portable
-   Composable
-   Version controlled

------------------------------------------------------------------------

# Summary

The proposed OKF architecture combines:

-   **Markdown** for knowledge representation
-   **YAML** for metadata
-   **Knowledge Graphs** for semantic relationships
-   **Vector Databases** for semantic retrieval
-   **Hybrid Search** (BM25 + Vector Search)
-   **LLMs and RAG** for intelligent question answering
-   **Git** as the primary version-controlled storage
-   **REST / GraphQL / MCP APIs** for interoperability

This architecture serves as a foundation for building an AI-native
knowledge management system that is portable, extensible, collaborative,
and optimized for modern retrieval and agentic AI workflows.
