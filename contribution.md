# Project Contribution

My primary focus in this project was the contextual retrieval pipeline and its integration into the application workflow.

## Text preparation

I prepared the source corpus by dividing documents into meaningful text segments using sentence tokenization and punctuation-aware boundaries. The goal was to avoid splitting passages in the middle of a complete thought and to create coherent inputs for context generation.

## Context generation

I integrated `Llama-3.2-1B-Instruct` to generate concise contextual descriptions for individual chunks. Each description summarized the chunk's topic and clarified its role within the broader document.

## Context-enriched retrieval

I appended each generated description to its original passage before indexing. This preserved the source text while adding semantic information that could help the retriever resolve ambiguous or incomplete chunks.

I tested the enriched representations to check whether:

- Generated descriptions remained aligned with the source passage
- Retrieved chunks matched the intent of the query
- Context enrichment supported more relevant retrieval
- The process avoided obvious semantic drift

## Interface collaboration

I also collaborated on the Streamlit interface and helped connect the contextual retrieval workflow to the user-facing comparison experience.

## Project scope

This was a collaborative academic project. The broader system also included regular chunking, late chunking, meta-chunking, FAISS and RocksDB infrastructure, evaluation dashboards, and additional interface components developed across the team.
