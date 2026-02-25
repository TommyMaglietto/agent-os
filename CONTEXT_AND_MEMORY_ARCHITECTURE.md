# Systems Engineering Specification for the V4 Delegation Machine
## A Unified Context and Memory Architecture

The realization of highly advanced, autonomous multi-agent software engineering systems necessitates a fundamental departure from monolithic context management. Traditional LLM applications treat context as an append-only log, a strategy that rapidly collapses under the weight of repository complexity. 

For the V4 Delegation Machine—a system predicated on a **Zero-Trust, Three-Branch constitutional framework**—the management of context is the primary mechanism of governance and operational integrity.

This architecture establishes a four-tier memory system designed to facilitate the seamless flow of information between the Legislative, Executive, and Judicial branches while maintaining a rigorous attention budget.

---

## The Constitutional Mandate: Zero-Trust Contextual Handoffs

In the V4 Delegation Machine, no branch possesses unfettered access to the internal "thought" streams or full episodic histories of another. 

Context is passed between branches through a standardized **Context Package**, mediated by the memory architecture.
*   **Legislative (Orchestrators)** retrieves relevant architectural context from Semantic Memory and initiates a task.
*   **Executive (Implementers)** consumes this context, performs work in sandboxed environments, and generates a refined episodic record.
*   **Judicial (Reviewers)** evaluates the artifacts against established Architectural Decision Records (ADRs), extracting "lessons learned" to update the permanent Semantic Memory.

---

## Tier I: Working Memory and the Virtual Context Manager (VCM)

Working Memory is the system's immediate attention window, analogous to a CPU's registers and primary cache. To address quadratic memory costs inherent in self-attention, we employ an OS-inspired **Virtual Context Manager (VCM)**.

### The RAM-Disk Analogy and Context Paging
The VCM treats the LLM's limited context window as "main memory" (RAM) and external vector/graph stores as "disk storage."
Agents actively "**page in**" relevant information from external storage via tool calls, and "**page out**" less critical data. This provides the illusion of an infinite context window. 

### Reducer-Driven State Management
State is a shared data structure (JSON/Python object) representing the system's snapshot. Updates are merged using reducer logic (e.g., list-append, atomic overwrite), ensuring safe, auditable, and atomic transitions between agents without overwriting data.

---

## Tier II: Episodic Memory and Trajectory Preservation

Episodic Memory captures sequential "experiences" (turns, tool calls, reasoning steps). It bridges transient Working Memory and permanent Semantic Memory.

### Checkpointing and Time-Travel Debugging
Robust checkpointing via SQLite/Redis/Postgres allows the Judicial branch to perform **Time-Travel Debugging**. A Reviewer can inspect the exact state at Step N to determine why an Implementer hallucinated.

### Cognitive Triage and Observation Masking
Repetitive outputs and raw logs rapidly pollute context. The V4 system uses **Observation Masking**:
*   Older tool outputs (e.g., >10 turns) are replaced with placeholders like `[Archived Observation]`. 
*   This alone typically reduces API costs by >50% and improves actual solve rates by removing noise.

### The "Pre-Compaction Flush"
Before working memory is masked, key facts, configurations, and success/failure signals are silently written to an ephemeral file (`MEMORY.md`), ensuring the "kernel of truth" remains accessible even after raw logs are pruned.

---

## Tier III: Semantic Memory and the Relational "Corporate Brain"

Semantic Memory is the permanent repository decoupled from any single session, housing architectural concepts, dependencies, and retrieved ADRs.

### The Hybrid GraphRAG Architecture
Traditional Vector RAG handles fuzzy semantic matching well, but struggles with code structure. The V4 system uses a **Hybrid GraphRAG** approach:
*   **Vectors:** Used for conceptual/"vibes" based questions.
*   **Graph Traversals (Cypher/Gremlin):** Used for hard dependency mapping ("Which 4 files depend on the authentication middleware?").
A Retrieval Router determines the optimal source dynamically.

### AST-Structured Code Intelligence
To move beyond simple text-based `grep`, the system parses codebases into **Abstract Syntax Trees (AST)** using tools like `tree-sitter`. This enables symbol-level indexing (classes, methods), preventing fragmentation and allowing safe resolution of function overloads or deeply nested modules.

### Judicial Learning and the ADR Loop
When the Judicial branch completes a review, it extracts failures and encodes them into **Architectural Decision Records (ADRs)** as permanent graph nodes. A failure related to a concurrency rule immediately becomes context for *every future task* in that module, creating a "moat" of self-correcting repository intelligence.

---

## Tier IV: The Context Funnel and Adaptive Pruning

The Funnel sits between expansive memory tiers and the model's finite attention window, compressing information down to its highest density.

### Task-Aware Adaptive Pruning (The Neural Skimmer)
When an agent requests a file, they pass a **Goal Hint** (e.g., "Focus on MRO resolution logic"). A lightweight localized neural skimmer (e.g., 0.6B parameters) scores each line of the requested file against the hint. 
Only relevant lines are returned to the agent, achieving up to 14.8x compression with zero loss of structural integrity. 

---

## Inter-Branch Dynamics and Context Handoff Protocols

Zero-Trust requires stringent transfer protocols, implemented via the **Agent2Agent (A2A)** standard.

### The Context Package Schema (JSON-RPC 2.0)
The Orchestrator does not send a natural language brief. It transmits a strict JSON object:
1.  **`Task Manifest`**: Unique ID and pointer to the execution plan.
2.  **`Environment Snapshot`**: Filtered relevant paths, recent PRs, and active ADRs.
3.  **`Goal Hint`**: Explicit instructions for the Context Funnel (pruner).
4.  **`Audit Trail`**: Provenance metadata for Judicial tracking.

### State Consistency and the Validation Gate
Between handoffs, a deterministic **Validation Gate** ensures the output matches the expected JSON string schema exactly. Malformed responses trigger an automatic bounded retry loop before the Reviewer ever sees the data.

---

## Conclusion
By adopting an OS-inspired virtual memory system, hybrid AST/Graph RAG capabilities, observation masking, and strict JSON protocol validation, the V4 Delegation Machine conquers the defining bottleneck of modern multi-agent systems: **context collapse.** 

This architecture guarantees peak density routing at every inference cycle, enabling flawless, autonomous repository-scale engineering.
