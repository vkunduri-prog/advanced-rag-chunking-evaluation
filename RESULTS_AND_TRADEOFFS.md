# Results and Trade-offs

## What the project demonstrated

The system successfully processed uploaded documents through several chunking strategies and displayed comparative outputs in a shared Streamlit interface.

The report described these broad findings:

- Regular chunking remained useful for simple, low-complexity use cases.
- Context enrichment improved retrieval alignment for ambiguous or incomplete passages.
- Meta-chunking created logical segments using perplexity, margin sampling, and dynamic merging.
- Late chunking preserved broader document context and was considered valuable for complex documents.
- FAISS and RocksDB supported reusable similarity search and persistent content access.
- The original Qwen generation path was too slow for interactive use in the available environment, motivating a faster API-based generation path.

## Exploratory runtime observations

The report's chart narrative described sample processing times ranging roughly from two to eight seconds across configurations and trials after the interactive system was established.

These values should be treated as exploratory because the report does not provide:

- Exact hardware specifications
- Corpus size for each run
- Model configuration
- Warm-up protocol
- Full raw measurements
- Statistical uncertainty

## Conflicting interpretations

Different report sections make conflicting statements about late chunking:

- One section interprets it as highly time/space efficient in the displayed trials.
- Another describes it as the most time-consuming and memory-intensive because it processes the full document context.

These statements can both occur under different implementations or measurement boundaries, but the report does not provide enough detail to reconcile them definitively.

Therefore, this portfolio does not claim that late chunking was universally fastest, slowest, most memory-efficient, or most accurate.

## Defensible conclusion

The main conclusion is a design trade-off:

| Strategy | Primary benefit | Primary risk |
|---|---|---|
| Regular | Simplicity and speed | Context loss |
| Contextual retrieval | Better chunk disambiguation | Additional generation cost and possible context noise |
| Meta-chunking | Logical, adaptive boundaries | Computational complexity |
| Late chunking | Long-range contextual preservation | Potentially expensive long-context processing |

The appropriate strategy depends on the document distribution, question complexity, update frequency, latency target, and available infrastructure.
