# Limitations

## Documentation-only repository

The original complete team source code and exact environment are unavailable, so this repository cannot reproduce the application.

## Academic prototype

The system was developed as an academic comparison framework, not as a hardened production service.

## Incomplete benchmark specification

The report does not fully specify:

- Hardware and operating environment
- Corpus size and composition for every trial
- Exact model versions and parameters
- Chunk sizes and overlaps for every strategy
- Retrieval depth
- Raw benchmark records
- Confidence intervals or statistical tests

## Exploratory quality assessment

Retrieval accuracy and generation quality were discussed, but the report does not include a complete labeled benchmark with standard metrics for all strategies.

## Conflicting resource conclusions

Some report sections interpret late chunking as efficient in the measured trials, while other sections describe it as computationally intensive. The missing raw data and measurement definitions prevent a definitive resolution.

## Generated contextual descriptions

Context enrichment can improve retrieval but may also:

- Add inaccurate framing
- Overemphasize one interpretation
- Increase ingestion cost
- Expand index size
- Become stale when source documents change

## Model and API dependency

The original interactive system changed generation backends because of local performance constraints. API-based generation introduces external cost, rate-limit, availability, and privacy considerations.
