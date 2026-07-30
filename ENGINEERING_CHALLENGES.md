# Engineering Challenges

## 1. Slow generation backend

The initial Qwen-based system could require up to approximately twenty minutes to generate one answer in the available environment.

**Response:** The team moved the interactive generation path to an OpenAI API-based model, substantially improving responsiveness.

**Lesson:** Model quality is only one system constraint. Hardware, latency, deployment environment, and user interaction requirements must influence model selection.

## 2. Context loss at chunk boundaries

Traditional segmentation can separate a statement from the section, entity, or event that gives it meaning.

**Response:** The project evaluated contextual descriptions, document-level embeddings, and logical segmentation techniques.

**Lesson:** Retrieval failures often originate during document preparation rather than during generation.

## 3. Comparing fundamentally different methods

Regular, contextual, late, and meta-chunking perform different amounts of work at different stages.

**Response:** The team used a shared document source and side-by-side interface.

**Remaining issue:** A rigorous benchmark must clearly separate ingestion time, indexing time, retrieval latency, and generation latency.

## 4. Persistent retrieval infrastructure

Vector search returns identifiers or positions, while applications also need the source text and metadata associated with those representations.

**Response:** FAISS handled similarity search and RocksDB supported persistent storage of linked document information.

## 5. Context-generation reliability

An LLM-generated description can clarify a chunk, but it can also introduce unsupported framing.

**Response:** Context descriptions were appended to, rather than substituted for, the original chunk and were tested for alignment.

**Future safeguard:** Add automated entailment checks and human-reviewed evaluation examples.
