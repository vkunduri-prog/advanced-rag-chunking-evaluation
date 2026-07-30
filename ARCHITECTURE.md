# System Architecture

## End-to-end flow

The project used a shared ingestion and retrieval architecture so the same uploaded documents could be processed through multiple chunking strategies and compared in one interface.

```mermaid
sequenceDiagram
    actor User
    participant UI as Streamlit UI
    participant Prep as Preprocessing
    participant Chunk as Chunking Strategy
    participant Index as FAISS Index
    participant Store as RocksDB
    participant LLM as Generative Model

    User->>UI: Upload document
    UI->>Prep: Extract and normalize text
    Prep->>Chunk: Send document text
    Chunk->>Chunk: Regular / contextual / late / meta processing
    Chunk->>Index: Store vector representations
    Chunk->>Store: Store text, metadata, and identifiers

    User->>UI: Submit query
    UI->>Index: Search nearest representations
    Index-->>UI: Relevant identifiers
    UI->>Store: Fetch chunk text and metadata
    Store-->>UI: Retrieved context
    UI->>LLM: Query + retrieved context
    LLM-->>UI: Grounded answer
    UI-->>User: Compare outputs and metrics
```

## Core components

### Document ingestion

The interface accepted uploaded text documents and initialized the reusable retrieval structures. A shared data source helped make comparisons more consistent across strategies.

### Chunking layer

The architecture supported four processing paths:

- Regular chunking
- Contextual retrieval
- Late chunking
- Meta-chunking

Each strategy transformed the same source material differently before retrieval.

### Retrieval layer

FAISS supported similarity search over document representations. RocksDB stored persistent text, metadata, and index-linked records needed to reconstruct retrieved context.

### Generation layer

The team initially experimented with Qwen, but generation could take up to approximately 20 minutes for one answer in the available environment. The project then used an OpenAI API-based model for a more responsive interactive workflow. Llama-3.2-1B-Instruct was also used in the contextual-retrieval path to generate contextual descriptions.

### Comparison interface

The Streamlit interface displayed strategy descriptions, outputs, processing time, and memory measurements in a side-by-side layout.
