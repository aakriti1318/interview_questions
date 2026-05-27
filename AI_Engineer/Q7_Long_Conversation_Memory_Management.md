
# AI Engineer Interview Question

## Topic: Memory Management for Long Conversations

---

### Question

> How would you design a memory system for an assistant that must maintain relevant context across very long multi-session conversations while keeping latency low and ensuring privacy? Describe storage, retrieval, and pruning strategies.

---

### Answer

Designing memory for long conversations involves a trade-off between relevance, retrieval speed, and privacy. The system should store compact, indexed representations and support efficient semantic retrieval with explicit retention controls.

---

#### Storage & Representations

1. Store both raw artifacts (when allowed by privacy policy) and dense embeddings derived from them. Use compressed embeddings or lower-dimensional representations for long-term storage.
2. Attach metadata: timestamps, user consent flags, topic tags, and sensitivity levels.

#### Retrieval Strategies

1. Use hierarchical retrieval: first a cheap keyword or tag filter, then a vector similarity search over embeddings, then an extractive reranker for top candidates.
2. Retrieve bounded context windows rather than all memory; merge with session context before inference.

#### Pruning & Retention

1. Implement tiered retention: short-term cache (fast, unpruned), medium-term store (prune by relevance decay), and long-term archive (highly compressed or policy-locked).
2. Use relevance scoring and recency to evict low-utility memories automatically, and provide explicit user controls to forget or export memory.

#### Privacy & Access Control

1. Encrypt storage at rest and implement strict RBAC for backend access.
2. Respect consent flags during retrieval; ensure queries automatically filter out memories marked as non-sharable.

#### Performance Considerations

1. Precompute and cache embeddings for frequent queries.
2. Use approximate nearest neighbor indices tuned for update frequency and latency targets.

---

#### What This Tests

- Knowledge of vector search and retrieval pipelines
- Designing privacy-aware persistent memory systems
- Trade-offs between latency, cost, and recall

