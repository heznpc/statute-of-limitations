# AI Agent Memory Systems: Forgetting/Expiration Mechanisms

Technical survey of how current AI memory systems handle data expiration, decay, and deletion.
Compiled for the statute-of-limitations paper.

---

## Classification Framework

Before surveying individual systems, we define four distinct mechanisms for handling aged memory:

| Mechanism | Definition | Data status | Reversible? |
|---|---|---|---|
| **DELETION** | Data physically removed from storage | Gone | No |
| **DECAY** | Data remains but retrieval weight decreases over time | Present, weakened | Yes (via reinforcement) |
| **ARCHIVAL** | Data moved to cold storage, accessible via explicit search | Present, relocated | Yes (via retrieval) |
| **AUTHORITY EXPIRATION** | Data present at full fidelity, but permission to act on it revoked | Present, intact | Possible (via reactivation) |

**Key finding: No surveyed system implements AUTHORITY EXPIRATION. This is the gap the paper addresses.**

---

## 1. Mem0 (arXiv 2504.19413)

**Paper**: "Mem0: Building Production-Ready AI Agents with Scalable Long-Term Memory" (April 2025)
**Source code**: github.com/mem0ai/mem0

### Architecture

Dual-store system: vector store (Qdrant) + graph store (Neo4j). Memory operations are LLM-mediated: an LLM evaluates incoming conversation against existing memories and selects one of four operations:

- **ADD**: Create new memory entry
- **UPDATE**: Augment/modify existing memory with new information
- **DELETE**: Remove contradictory or outdated memory
- **NOOP**: No modification required

### Expiration Mechanism

The `expiration_date` parameter is a metadata field set at write time using ISO 8601 format:

```python
expiration_date = (datetime.now() + timedelta(days=7)).isoformat()
m.add(messages, user_id="user1", metadata={"expiration_date": expiration_date})
```

**What happens on expiry**: The memory is **automatically DELETED** from the active store. Mem0 documentation explicitly states: "Memories with expiration_date are automatically removed after expiring." No background cron job is needed; the cleanup is handled transparently by the system.

### What is NOT implemented

- No severity-based or type-based differentiated TTL (the developer must manually set different expiration_dates per memory)
- No archival of expired memories (they are removed, not moved)
- No decay function (memories are either fully present or fully deleted)
- No reactivation mechanism for expired memories

### Known Bug: Incomplete Deletion

GitHub Issue #3245 reveals that `_delete_memory()` only cleans up the vector store (Qdrant) and history database, but **does not clean up the graph store (Neo4j)**. This creates orphaned nodes: one user reported 2,600 active Qdrant memories but 2,700+ Neo4j nodes/relationships. The `delete_all()` method partially mitigates this, but individual deletions leave graph residue.

**Ironic parallel**: Even in a system designed for clean deletion, complete erasure proves technically difficult. This echoes Eco's paradox and machine unlearning failures.

### Classification: **DELETION** (intended), with accidental partial persistence (graph residue)

---

## 2. MemOS (arXiv 2507.03724, May-July 2025)

**Paper**: "MemOS: A Memory OS for AI System" (MemTensor)

### Architecture

Three memory types unified under a MemCube abstraction:
- **Parametric memory**: Model weights
- **Activation memory**: KV-cache
- **Plaintext memory**: External text/structured data

Core components: MemReader, MemScheduler, MemLifecycle, MemOperator, MemGovernance, MemVault

### Memory Lifecycle: Five States

Each memory unit transitions through a state machine:

```
Generated → Activated → Merged → Archived → Expired
```

| State | Trigger | Data Status |
|---|---|---|
| **Generated** | Initial creation/ingestion | Active, accessible |
| **Activated** | High access frequency ("hot" data) | Promoted, prioritized |
| **Merged** | Repeated user confirmations or structural integration | Consolidated into canonical knowledge |
| **Archived** | Policy, user command, or scheduling (infrequent access) | Moved to cold storage (MemVault), still accessible |
| **Expired** | TTL expiration or policy-defined rules | Access restricted, not physically deleted |

### Critical Detail: Expiration != Deletion

MemOS explicitly distinguishes archival from expiration, and neither involves physical deletion:

- **Archived**: "Keeping frequently accessed data active and less-used data cold or long-term stored." Data moves to MemVault with retained governance policies and version chains.
- **Expired**: Access is **restricted through policy-driven gating**, not physical removal. Expired memories "remain queryable for audit/compliance purposes." Governed by ACL (Access Control List), TTL, and conditional activation policies.
- **Reclamation**: A separate resource cleanup phase, controlled by governance policies rather than automatic deletion.

### Type-Based Differentiation

MemOS is the only surveyed system with explicit type-based lifecycle differentiation:

- **Parametric memory**: Long-term stability; transitions from Activated directly to Archived through scheduled distillation
- **Activation memory (KV-Cache)**: Rapid cycling; frequent activation/expiration for multi-turn dialogue
- **Plaintext memory**: Policy-flexible; supports conflict detection, deduplication, versioning, and forgetting policies with user-defined TTLs

### Governance Layer

MemGovernance enforces:
- Sensitivity tags and watermarks
- Access Control Lists per memory unit
- Compliance and traceability logging
- Conditional activation policies (role-based and task-context-based)

### Classification: **ARCHIVAL** + rudimentary **AUTHORITY EXPIRATION** (access restricted, data persists)

**This is the closest existing system to the statute-of-limitations model, though it lacks severity-proportional TTL, reactivation mechanisms, suspension conditions, and non-retroactivity.**

---

## 3. Governed Memory (arXiv 2603.17787, March 2026)

**Paper**: "Governed Memory: A Production Architecture for Multi-Agent Workflows"

### Decay Function

Implements **exponential recency decay** with a configurable half-life:

> "Retrieval applies exponential recency decay (half-life = 38 days) to rank recent facts above outdated ones."

The implied formula (standard exponential decay):

```
score_adjustment = (0.5) ^ (t / 38)
```

Where t = days since memory creation. At 38 days, a memory's retrieval score is multiplied by 0.5; at 76 days, by 0.25; at 114 days, by 0.125.

### What Happens to Decayed Memories

**Memories are NOT deleted.** The decay function reduces their ranking score during retrieval, not their existence. However, a background consolidation process (described in Appendix D) can prune stale entries with safeguards:

> "An optional sole-memory protection ensures no entity is left with zero open-set memories. If all memories for an entity are older than the retention cutoff, the most recent is preserved."

### Conflict Resolution

For contradictory facts (stale vs. fresh), the system uses recency-based ranking:
- Tested with 30 conflict pairs: stale claims 74-270 days old vs. fresh claims 0-57 days old
- **83.3% conflict detection** (fresh information surfaced correctly)
- Only **33.3% full suppression** of stale content due to semantic overlap in keyword-based evaluation

### What is NOT implemented

- No severity-based or type-based differentiation (uniform 38-day half-life for all memory types)
- No suspension or reactivation mechanisms
- No authority layer distinct from retrieval weight

### Classification: **DECAY** (primary) + optional **DELETION** (background pruning with sole-memory protection)

---

## 4. Zep (arXiv 2501.13956, January 2025)

**Paper**: "Zep: A Temporal Knowledge Graph Architecture for Agent Memory"
**Engine**: Graphiti (temporal knowledge graph)

### Architecture

Three-tier knowledge graph:
- Episode subgraph (raw conversation episodes)
- Semantic entity subgraph (extracted entities and relationships)
- Community subgraph (higher-level clusters)

### Bi-Temporal Model

Zep tracks four timestamps on every edge (fact):

| Timestamp | Timeline | Meaning |
|---|---|---|
| `t'_created` | T' (ingestion) | When the fact entered the system |
| `t'_expired` | T' (ingestion) | When the fact was invalidated in the system |
| `t_valid` | T (world) | When the fact was actually true in the world |
| `t_invalid` | T (world) | When the fact ceased to be true in the world |

### Fact Invalidation Mechanism

When new information contradicts an existing fact:

1. LLM compares new edges against semantically related existing edges
2. If temporal contradiction detected, the system sets `t_invalid` of the old edge to `t_valid` of the new edge
3. **"Graphiti consistently prioritizes new information when determining edge invalidation"**

**Critical detail: Facts are MARKED INVALID, not deleted.** The system explicitly preserves "historical records of relationship evolution over time," maintaining "both current relationship states and historical records."

### What Zep Does NOT Have

- **No temporal decay function**: No recency weighting in retrieval scoring
- **No automatic aging**: Facts are binary (valid/invalid), not gradually weakened
- **No episode invalidation**: Only edges (facts) can be invalidated; episodes remain as "non-lossy data stores"
- **No TTL or expiration**: Invalidation is event-driven (new contradicting fact), not time-driven

### Classification: **Fact invalidation** (a form of AUTHORITY EXPIRATION at the edge level, but triggered by contradiction rather than time)

**Zep is architecturally interesting because it separates temporal validity from physical existence. However, invalidation is event-driven (new contradicting information), not time-driven (expiration after a period). It has no concept of "time served" leading to expiration.**

---

## 5. LangChain / LlamaIndex Memory

### LangChain Memory Types (Legacy, deprecated v0.3.1+)

| Memory Type | Mechanism | What Happens to Old Data |
|---|---|---|
| **ConversationBufferMemory** | Stores full conversation history | Unbounded growth until context limit; then truncated (DELETED) |
| **ConversationBufferWindowMemory** | Keeps last k exchanges | Oldest exchanges silently dropped (DELETED) |
| **ConversationSummaryMemory** | LLM summarizes conversation history | Original messages replaced by summary (LOSSY COMPRESSION) |
| **ConversationSummaryBufferMemory** | Hybrid: recent messages verbatim, older messages summarized | Messages beyond `max_token_limit` are summarized then dropped from buffer |
| **ConversationTokenBufferMemory** | Token-limited buffer | Oldest tokens dropped when limit exceeded (DELETED) |

**All LangChain legacy memory types implement DELETION through truncation. No decay, no archival, no authority expiration.**

Modern approach (LangGraph, 2025+): Persistent memory via checkpointing with message trimming functions and summary graph nodes. Still fundamentally buffer-based truncation.

### LlamaIndex Memory Types

| Memory Type | Mechanism | What Happens to Old Data |
|---|---|---|
| **ChatMemoryBuffer** | Token-limited buffer of recent messages | Oldest messages dropped OR flushed to long-term memory |
| **ChatSummaryMemoryBuffer** | Hybrid buffer + summarization | Oldest messages beyond `chat_history_token_ratio` are flushed and summarized |

LlamaIndex's advanced `Memory` class supports flushing old messages to long-term memory blocks (vector stores, fact extraction) rather than pure deletion. This provides an ARCHIVAL pathway, but only if explicitly configured.

### Classification: **DELETION** (default) with optional **ARCHIVAL** (LlamaIndex long-term memory blocks)

---

## 6. ChatGPT Memory (OpenAI)

### Architecture (as of April 2025 update)

Two distinct memory systems:

1. **Saved Memories**: Explicit factual entries (name, preferences, goals). Stored separately from chat history. Persist until manually deleted.
2. **Chat History Reference**: ChatGPT can reference all past conversations for context. Free users get short-term continuity; Plus/Pro users get longer-term understanding.

### Expiration/Deletion Mechanism

- **Saved Memories**: No automatic expiration. Persist indefinitely until user explicitly deletes them or tells ChatGPT to "forget" something.
- **Chat History**: "Details from past chats can change over time as ChatGPT updates what's more helpful to remember." The exact mechanism is opaque.
- **Manual Deletion**: Users can delete individual memories, clear all memories, or disable memory entirely.

### Post-Deletion Retention

> "OpenAI may retain a log of deleted Saved Memories for up to 30 days for safety and debugging purposes."

This is a **tombstone-like** retention: the memory is removed from the active system but a log persists in a separate safety/audit store for 30 days before true deletion.

**Architectural note**: Deleting a chat does NOT delete saved memories that were created during that chat. To fully erase a memory, both the saved memory entry AND the originating chat must be separately deleted.

### What is NOT Implemented

- No automatic decay or aging
- No severity-based retention (all saved memories treated equally)
- No archival tier (binary: present or deleted)
- No reactivation mechanism
- No transparency about internal chat history summarization

### Classification: **DELETION** (user-initiated) with **30-day tombstone retention** (safety log)

---

## 7. Claude Memory (Anthropic)

### Architecture

Two distinct systems:

#### 7a. Claude Consumer Memory (claude.ai, September-October 2025)

- Opt-in feature (off by default) for Team, Enterprise, Pro, and Max subscribers
- Claude can automatically save relevant information across conversations
- Users can view, edit, and delete saved memories
- "Incognito mode" prevents any memory formation
- Memories can be downloaded and exported to other chatbots
- **No documented automatic expiration, decay, or aging mechanism**

#### 7b. Claude API Memory Tool (`memory_20250818`)

- Client-side tool: Claude makes tool calls, the developer's application executes file operations
- Memories stored as **plain text files** (typically Markdown) in a `/memories` directory
- Operations: `view`, `create`, `str_replace`, `insert`, `delete`, `rename`
- **No automatic expiration built into the tool itself**

The API documentation explicitly suggests as a best practice:

> "Memory expiration: Consider clearing out memory files periodically that haven't been accessed in an extended time."

But this is a recommendation to developers, not a built-in mechanism.

#### 7c. Claude Code Memory (CLAUDE.md)

- Plain Markdown files read at session start
- Three hierarchy levels: project root (`./CLAUDE.md`), user global (`~/.claude/CLAUDE.md`), user project-specific
- **No automatic expiration, decay, or deletion whatsoever**
- Files persist indefinitely in the filesystem/git repository
- Content is injected into system prompt at every session start
- No mechanism to reduce influence of stale content

### Classification: **No forgetting mechanism at all** (pure persistence)

**Claude's approach is the Confucian model from the paper's taxonomy: total retention with no built-in forgetting. The burden of memory governance falls entirely on the user/developer.**

---

## 8. Letta (formerly MemGPT, arXiv 2310.08560)

**Paper**: "MemGPT: Towards LLMs as Operating Systems" (October 2023)

### Architecture: OS-Inspired Memory Hierarchy

Three tiers modeled on the CPU register / RAM / disk hierarchy:

| Tier | Analogy | Capacity | Persistence | Agent Access |
|---|---|---|---|---|
| **Core Memory** | CPU registers | Small, fixed | Always in context window (system prompt) | Direct read/write |
| **Recall Memory** | RAM | Medium | Searchable conversation history | Search via tool calls |
| **Archival Memory** | Disk | Unlimited | Vector DB of processed/indexed information | Search via tool calls |

### Self-Editing Memory

The agent itself decides what to remember via function calls during its reasoning loop:
- `core_memory_append(field, content)`: Add to core memory
- `core_memory_replace(field, old, new)`: Edit core memory
- `archival_memory_insert(content)`: Write to archival storage
- `archival_memory_search(query)`: Retrieve from archival storage
- `conversation_search(query)`: Search recall memory

### Eviction Mechanism

When context window approaches capacity:

1. Oldest messages in the conversation buffer are selected for eviction
2. These messages undergo **recursive summarization**: they are summarized along with existing summaries from previously evicted messages
3. The summary is retained; original messages are removed from the active context
4. **But all original messages persist in recall memory** (the database)

> "In Letta, all state—includes memories, user messages, reasoning, tool calls—are all persisted in a database, so they are never lost, even once evicted from the context window."

### What is NOT Implemented

- No automatic decay or time-based aging
- No TTL or expiration dates
- No severity-based differentiation (the agent treats all information equally)
- No policy-driven governance layer
- Eviction is capacity-driven, not time-driven

### Classification: **ARCHIVAL** (context eviction moves data to searchable storage; nothing is ever truly deleted)

**Letta's key insight: eviction from active context != deletion from the system. All data persists permanently in the database. The only "forgetting" is removal from the active context window, and even that is mitigated by summarization.**

---

## 9. Additional Systems

### 9a. MemoryBank (arXiv 2305.10250, May 2023)

**The only system implementing biologically-inspired forgetting.**

Ebbinghaus forgetting curve formula:

```
R = e^(-t/S)
```

Where:
- R = retention (probability of recall)
- t = time elapsed since last access
- S = memory strength (integer, initialized at 1)

**Reinforcement mechanism**: When a memory is recalled during conversation, S increments by 1 and t resets to 0. This makes the forgetting curve less steep for frequently-accessed memories.

**What happens below threshold**: The paper states this is "an exploratory and highly simplified memory updating model." No explicit deletion threshold is specified. Memories with low R are deprioritized in retrieval, not deleted. The mechanism "permits the AI to forget and reinforce memory based on time elapsed and the relative significance."

### Classification: **DECAY** (biologically-inspired, with reinforcement)

### 9b. Redis Agent Memory Server (2025)

Configurable forgetting with three strategies:

| Parameter | Default | Function |
|---|---|---|
| `FORGETTING_ENABLED` | false | Master toggle |
| `FORGETTING_EVERY_MINUTES` | 60 | Check frequency |
| `FORGETTING_MAX_AGE_DAYS` | (unset) | Hard age limit for deletion |
| `FORGETTING_MAX_INACTIVE_DAYS` | (unset) | Inactivity-based deletion |
| `FORGETTING_BUDGET_KEEP_TOP_N` | (unset) | Keep only N most recent memories |

When both age and inactivity thresholds are set, memories must be both old AND inactive to be deleted, unless they exceed a hard limit (max_age_days * hard_age_multiplier).

Working memory has automatic 1-hour TTL. Long-term memories use configurable forgetting.

### Classification: **DELETION** (configurable, with dual-threshold logic)

### 9c. Google Vertex AI Memory Bank (2025)

Two memory types:
- **Episodic Memory**: Narrative summaries stored as vector embeddings in Vertex AI Vector Search
- **Structured Preferences**: Key-value pairs in Firestore

TTL can be set at the memory resource level (up to 365 days). When TTL expires, **memories are automatically deleted**. The system "only persists information that is judged to be valuable for future interactions" at write time.

### Classification: **DELETION** (TTL-based)

### 9d. AMV-L: Adaptive Memory Value Lifecycle (arXiv 2603.04443, March 2026)

Assigns each memory item a "continuously updated utility score" and uses "value-driven promotion, demotion, and eviction to maintain lifecycle tiers." Retrieval is "restricted to a bounded, tier-aware candidate set that decouples the request-path working set from total retained memory."

Full technical details not available from abstract alone.

### Classification: Likely **ARCHIVAL** (tier-based, value-driven)

---

## 10. Cross-Cutting Analysis

### The "Soft Expiration" Gap

No surveyed system implements what might be called "soft expiration" — where data exists at full fidelity but its influence on agent behavior is reduced to exactly zero through an authority mechanism rather than a decay function.

The closest approximations:

| System | Approximation | Why it falls short |
|---|---|---|
| MemOS (Expired state) | Access restricted by policy | No reactivation mechanism; no severity proportionality |
| Zep (fact invalidation) | Old facts marked invalid | Event-driven, not time-driven; no graduated expiration |
| Governed Memory (decay) | Retrieval weight approaches zero | Asymptotic — never reaches exactly zero; no authority layer |
| MemoryBank (Ebbinghaus) | Retention probability decreases | Same asymptotic problem; no hard authority cutoff |

### Separation of Storage from Retrieval Authority

Only two systems partially separate these concerns:

1. **MemOS**: MemGovernance enforces ACL-based access control per memory unit, and expired memories remain queryable for audit. However, this is access control, not authority expiration in the legal sense.

2. **Zep**: Bi-temporal model separates "when the system learned this" from "when this was true in the world." Invalidated facts are preserved but excluded from active retrieval. However, invalidation is contradiction-driven, not time-driven.

No system separates "this information is stored and retrievable" from "this information may be used to make decisions" as a first-class architectural distinction.

### Type-Based Differentiated Retention

| System | Differentiation |
|---|---|
| MemOS | Yes — parametric/activation/plaintext have different lifecycle patterns |
| Mem0 | No — developer must manually set different expiration_dates |
| Governed Memory | No — uniform 38-day half-life for all types |
| Zep | No — all facts governed by same invalidation logic |
| Letta | No — agent treats all information equally |
| ChatGPT | No — all saved memories treated equally |
| Claude | No — all CLAUDE.md content has equal weight |
| LangChain/LlamaIndex | No — buffer limits apply uniformly |
| Redis AMS | No — forgetting thresholds are per-namespace, not per-type |

**Only MemOS offers type-based differentiation, and even there it is based on memory modality (parametric vs. activation vs. plaintext), not semantic severity (safety-critical vs. preference vs. ephemeral).**

### Tombstone Pattern Parallel

In distributed databases (Cassandra, Bigtable), tombstones are lightweight timestamped markers that represent deletion without physically removing data:

- **Purpose**: Propagate delete operations across replicas while maintaining eventual consistency
- **Mechanism**: Insert a deletion marker; suppress the record in reads; physically remove during compaction after a grace period (`gc_grace_seconds`)
- **Key property**: The data is "functionally deleted" (invisible to queries) but physically present until compaction

**AI memory parallel**: ChatGPT's 30-day retention of deleted memory logs is the closest to a tombstone pattern. Zep's fact invalidation (setting `t_invalid`) is structurally identical to a tombstone — a marker that says "this fact is no longer current" without removing the underlying data.

**Distinction from statute of limitations**: Tombstones are temporary markers pending physical deletion. The statute-of-limitations model proposes that the "tombstone" is permanent — data persists forever, but its authority to influence decisions is permanently (or at least durably) revoked, with possible reactivation under specific conditions.

---

## 11. Summary Table

| System | Mechanism | Data after expiry | Time-based? | Type-differentiated? | Reactivation? |
|---|---|---|---|---|---|
| Mem0 | DELETION | Gone (vector); residue (graph) | Yes (TTL) | No | No |
| MemOS | ARCHIVAL + policy gating | Present, access-restricted | Yes (TTL/decay) | Yes (by modality) | Not documented |
| Governed Memory | DECAY + optional pruning | Present, downweighted | Yes (38-day half-life) | No | No |
| Zep | Fact invalidation | Present, marked invalid | No (event-driven) | No | No |
| LangChain | DELETION (truncation) | Gone | No (capacity-driven) | No | No |
| LlamaIndex | DELETION or ARCHIVAL | Gone or in long-term store | No (capacity-driven) | No | No |
| ChatGPT | DELETION + 30-day log | Gone (30-day safety log) | No (user-initiated) | No | No |
| Claude | No mechanism | Always present | No | No | N/A |
| Letta | ARCHIVAL (context eviction) | Present in recall/archival DB | No (capacity-driven) | No | Yes (via search) |
| MemoryBank | DECAY (Ebbinghaus) | Present, deprioritized | Yes (continuous decay) | No | Yes (via recall reinforcement) |
| Redis AMS | DELETION | Gone | Yes (configurable) | No | No |
| Google Vertex | DELETION | Gone | Yes (TTL) | No | No |

---

## 12. Implications for the Paper

The survey reveals a clear pattern:

1. **The dominant paradigm is DELETION.** Most systems (Mem0, LangChain, ChatGPT, Redis, Google Vertex) treat forgetting as physical removal of data. This is the "forget = delete" assumption the paper challenges.

2. **DECAY is rare and unsophisticated.** Only Governed Memory and MemoryBank implement time-based decay, and both use uniform functions with no severity differentiation.

3. **ARCHIVAL exists but lacks governance.** Letta and MemOS move data rather than delete it, but neither implements a principled authority layer that separates "this data exists" from "this data may influence decisions."

4. **No system implements the statute-of-limitations model** — where information persists at full fidelity, authority to act on it expires based on severity-proportional timelines, suspension conditions can pause the clock, new evidence can reactivate expired authority, and policy changes are non-retroactive.

5. **MemOS is the closest precursor**, with its five-state lifecycle and policy-driven access gating for expired memories. But it lacks severity proportionality, reactivation conditions, suspension logic, and non-retroactivity guarantees.

6. **Zep's bi-temporal model provides useful infrastructure** (separating system time from world time, preserving historical records), but its invalidation is event-driven rather than time-driven.

7. **The tombstone pattern from distributed databases** provides a more precise analogy than TTL for what the paper proposes — but tombstones are temporary pending physical deletion, whereas the statute-of-limitations model proposes permanent data persistence with permanent (but potentially reversible) authority expiration.

---

## Sources

### Primary Papers
- Mem0: arXiv 2504.19413 (April 2025)
- MemOS: arXiv 2507.03724 (July 2025) / arXiv 2505.22101 (May 2025)
- Governed Memory: arXiv 2603.17787 (March 2026)
- Zep: arXiv 2501.13956 (January 2025)
- MemGPT/Letta: arXiv 2310.08560 (October 2023)
- MemoryBank: arXiv 2305.10250 (May 2023)
- AMV-L: arXiv 2603.04443 (March 2026)

### Documentation
- Mem0 docs: docs.mem0.ai/cookbooks/essentials/memory-expiration-short-and-long-term
- Mem0 GitHub Issue #3245: Memory deletion does not clean up Neo4j graph data
- Letta docs: docs.letta.com/advanced/memory-management/
- Claude Memory Tool: platform.claude.com/docs/en/agents-and-tools/tool-use/memory-tool
- Claude Code Memory: code.claude.com/docs/en/memory
- OpenAI Memory FAQ: help.openai.com/en/articles/8590148-memory-faq
- Redis Agent Memory Server: redis.github.io/agent-memory-server/memory-lifecycle/
- Google Vertex AI Memory Bank: cloud.google.com/agent-builder/agent-engine/memory-bank/overview
- LangChain ConversationBufferMemory: python.langchain.com/docs/versions/migrating_memory/
- LlamaIndex Memory: developers.llamaindex.ai/python/framework/module_guides/deploying/agents/memory/

### Database Patterns
- Tombstone (data store): en.wikipedia.org/wiki/Tombstone_(data_store)
- Cassandra tombstones: cassandra.apache.org/doc/latest/cassandra/managing/operating/compaction/tombstones.html
