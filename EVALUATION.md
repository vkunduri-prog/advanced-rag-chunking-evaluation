# Evaluation Design

## Evaluation questions

The project investigated:

1. Does a strategy retrieve content that is relevant to the question?
2. Does the retrieved context preserve enough information to support a grounded answer?
3. How does preprocessing and retrieval time differ across strategies?
4. How much memory does each configuration use?
5. What quality-efficiency trade-offs appear in side-by-side use?

## Dimensions

### Retrieval relevance

The team compared whether returned chunks matched the subject and intent of a query. Contextual retrieval was tested against non-enriched chunks to examine whether contextual descriptions improved alignment.

### Generation quality

Answers were inspected for:

- Relevance
- Coherence
- Contextual completeness
- Alignment with retrieved evidence
- Handling of questions requiring information across sections

### Processing time

Execution time was recorded across repeated trials for the baseline and advanced configurations.

### Memory usage

Memory measurements were collected for the main, contextual-retrieval, late-chunking, and meta-chunking paths.

### Time-to-memory ratio

A combined exploratory ratio was visualized to compare resource efficiency. This was a project-specific diagnostic, not a standard RAG benchmark.

## Recommended production metrics

A future reproducible version should add:

- Recall@k
- Precision@k
- Mean Reciprocal Rank
- nDCG
- Context precision
- Context recall
- Faithfulness or groundedness
- Answer relevance
- End-to-end p50, p95, and p99 latency
- Peak resident memory
- Ingestion cost per document
- Generation cost per query

## Benchmark protocol

A stronger protocol would:

1. Create a labeled set of documents, questions, relevant passages, and reference answers.
2. Freeze model, hardware, chunk-size, retrieval-depth, and prompt settings.
3. Run each strategy multiple times.
4. Report averages, dispersion, and confidence intervals.
5. Separate ingestion performance from query-time performance.
6. Evaluate both retrieval and answer generation.
