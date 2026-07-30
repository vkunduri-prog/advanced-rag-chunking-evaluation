# Chunking Strategies

## Regular chunking

Regular chunking splits a document before embedding. Boundaries may be based on sentence, token, character, or fixed-length rules.

**Strengths**

- Straightforward to implement
- Low preprocessing complexity
- Suitable for simple documents and direct questions
- Easy to update individual chunks

**Risks**

- Cross-section relationships may be lost
- Pronouns or references may become ambiguous
- Retrieval quality is highly sensitive to chunk size and overlap

## Contextual retrieval

Contextual retrieval enriches each chunk with a concise description of its role in the larger document.

Example:

```text
Original:
"The model was replaced because a single answer required approximately
twenty minutes."

Context:
"This passage explains why the project changed its generative backend
during performance optimization."
```

The combined representation gives retrieval algorithms both the detailed passage and a higher-level semantic cue.

**Strengths**

- Helps disambiguate locally incomplete passages
- Preserves the original chunk text
- Can improve retrieval for vague or indirect queries
- Works with conventional indexing infrastructure

**Costs**

- Requires an additional LLM call during ingestion
- Generated descriptions may introduce noise
- Indexing time and token usage increase

## Late chunking

Late chunking processes a longer document context before deriving span-level chunk vectors. In the project, a Jina embedding model and span annotations were used to create pooled representations.

**Strengths**

- Preserves long-range semantic context
- Useful when related information appears in distant sections
- Can improve retrieval for complex cross-document questions

**Costs**

- Long-context processing can be expensive
- Document updates may require substantial reprocessing
- Memory and runtime depend heavily on document length and hardware

## Meta-chunking

Meta-chunking attempts to find logical transitions rather than relying only on fixed lengths. The project used:

- Perplexity-based boundary detection
- Margin sampling between adjacent sentences
- Dynamic merging of smaller logical units

**Strengths**

- Produces semantically coherent sections
- Adapts to mixed document structures
- Balances granular retrieval with broader context

**Costs**

- More complex than fixed segmentation
- Perplexity calculations can be computationally expensive
- Thresholds may need dataset-specific tuning

## Selection guidance

| Requirement | Likely starting point |
|---|---|
| Low latency and simple documents | Regular chunking |
| Ambiguous passages needing document context | Contextual retrieval |
| Long documents with cross-section dependencies | Late chunking |
| Heterogeneous documents with logical transitions | Meta-chunking |

No strategy is universally best. A robust production system should benchmark each method on representative documents and questions.
