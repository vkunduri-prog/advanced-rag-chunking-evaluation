# Contextual Retrieval Pipeline

This document describes the part of the project I primarily contributed to.

## Objective

The contextual-retrieval path addressed a common RAG failure mode: a chunk can be relevant in its original document but become ambiguous after it is separated from neighboring content.

The solution was to add a short, generated context statement to each chunk before indexing.

## Processing stages

### 1. Corpus preparation

The text corpus was divided into meaningful units using:

- Sentence tokenization
- Punctuation-aware segmentation
- Logical text boundaries where possible

The goal was to avoid splitting in the middle of a complete thought.

### 2. Context generation

`Llama-3.2-1B-Instruct` generated a concise description for each chunk. The description explained what the passage represented in the larger document.

Conceptual prompt:

```text
Given the document context and the selected passage, write a concise
description explaining the passage's role and subject. Do not add facts
that are absent from the source.
```

### 3. Context enrichment

The description was appended to the original text rather than replacing it.

```text
enriched_chunk =
    contextual_description
    + "\n\n"
    + original_chunk
```

This preserved source detail while adding retrieval-oriented semantic information.

### 4. Representation and indexing

The enriched chunks were transformed with TF-IDF and stored in a FAISS similarity index. Associated text and metadata were persisted through RocksDB in the wider team architecture.

### 5. Query retrieval

A user query was embedded into the same representation space. FAISS identified the closest enriched chunks, after which the original/contextual text could be supplied to the answer-generation model.

## Validation approach

Testing focused on whether:

- Context descriptions accurately represented the source passage
- Enrichment improved the match between queries and relevant chunks
- Retrieved content remained grounded in the source
- Generated descriptions avoided introducing unsupported information
- The pipeline integrated correctly with the Streamlit comparison interface

## Important design choice

The generated context should support retrieval, not become a substitute for evidence. The original passage must remain available to the answer-generation model and to any evaluator checking source grounding.
