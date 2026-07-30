# Future Work

## Reproducible benchmark suite

Build a labeled dataset containing:

- Source documents
- User questions
- Relevant chunk identifiers
- Reference answers
- Multi-hop and ambiguous questions

Evaluate every strategy with identical models, retrieval depth, prompts, and hardware.

## Adaptive strategy routing

Use document and query characteristics to select a chunking method dynamically.

Examples:

- Direct factual query → regular chunking
- Ambiguous local passage → contextual retrieval
- Cross-section synthesis → late chunking
- Heterogeneous document structure → meta-chunking

## Hybrid retrieval

Combine dense semantic vectors with sparse lexical retrieval and reranking. This can protect exact entities, numbers, and terminology that may be weakened in purely semantic representations.

## Context-quality gates

Before indexing an LLM-generated description:

1. Check semantic similarity to the original passage.
2. Detect unsupported entities or claims.
3. Reject descriptions that materially alter meaning.
4. Retain provenance linking the description to source text.

## Strategy-level observability

Track:

- Ingestion duration
- Index size
- Query latency
- Retrieved source identifiers
- Retrieval scores
- Prompt token count
- Answer groundedness
- Cost per document and per query

## Incremental updates

Design an update path that avoids recomputing an entire corpus when one document changes, especially for late-chunking configurations.

## User-facing evidence

Display source passages and document metadata next to generated answers so users can verify the retrieved evidence.
