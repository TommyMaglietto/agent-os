# Master AI Agent Procedures: The Ultimate Delegation Machine (V4)

## Overview
This document represents the absolute pinnacle of autonomous AI software engineering. It evolves the architecture from a simple delegation pipeline into a **flawless, self-healing, zero-trust ecosystem**. 

By enforcing strict separation of powers, self-modifying protocols, and automated deadlock resolution, this system guarantees that no hallucination, regression, or architectural flaw makes it into production.

---

## 1. Zero-Trust Agent Architecture

In a perfect system, no agent trusts another agent's output. Every handoff is treated as potentially contaminated until cryptographically or algorithmically verified.

### 1.1. The 3-Branch Separation of Powers
Agents are strictly firewalled. An agent may only operate within its assigned branch for a given task cycle to prevent "marking its own homework."

*   **Branch 1: The Legislative (Planning & Architecture)**
    *   **Actors:** Orchestrator, Architecture Reviewer, Context Manager.
    *   **Mandate:** Define the exact scope, security boundaries, and bite-sized steps. They produce the "Constitutional Plan."
    *   **Restriction:** **Forbidden** from writing implementation code.
*   **Branch 2: The Executive (Implementation)**
    *   **Actors:** Frontend, Backend, API Specialists.
    *   **Mandate:** Execute the exact micro-tasks defined by the Legislative branch in isolated Git Worktrees.
    *   **Restriction:** Cannot modify the architecture or accept their own code. If a plan is technically impossible, they must issue a formal "Rejection Ticket" back to the Legislative branch rather than improvising.
*   **Branch 3: The Judicial (Verification & Audit)**
    *   **Actors:** Code Reviewer, Security Analyzer, QA Automation.
    *   **Mandate:** The final gatekeepers. They cross-examine the Executive's code against the Legislative's plan.
    *   **Restriction:** Cannot write fixes. They only issue "Pass" or "Reject with Subpoena" (detailed failure logs).

---

## 2. Meta-Cognition & Self-Healing Pipelines

A perfect machine doesn't just write code; it writes the software that writes the code.

### 2.1. The Self-Modifying System
*   **Dynamic Prompt Generation:** Hardcoded prompts degrade over time. The Orchestrator does not use generic prompts to brief the Executive branch. It dynamically compiles a unique, hyperspecific instruction set for every single micro-task based on the current AST (Abstract Syntax Tree) and latest Knowledge Items (KIs).
*   **Skill Factory:** If an agent executes essentially the same troubleshooting loop 3 times across a project, it is flagged. The `Skill Creator` agent is automatically dispatched to write a new `SKILL.md` and Python script to automate that exact bottleneck for the future.

### 2.2. Autonomous State Management (The Pre-Flight Protocol)
Code synthesis cannot begin until the system has successfully traversed the Pre-Flight logic gates:
1.  **Context Matrix Gate:** `Context Manager` prunes the codebase down to the exact 4-5 files required. Large files are segmented.
2.  **Red Team Gate (`/ultra-think`):** The `Architecture Reviewer` intentionally attempts to break the Orchestrator's proposed plan (looking for OWASP vulnerabilities, race conditions, or N+1 queries).
3.  **TDD Commitment Gate:** The Judicial branch writes and commits the failing integration tests *before* the Executive branch is granted access to the workspace.

---

## 3. Absolute Execution & Deadlock Protocols

### 3.1. The "Two-Key" Protocol
No code merges to `main` without verifiable approval from BOTH:
1.  An Executive implementer (local tests pass).
2.  An Independent Judicial reviewer (global tests, linting, security scans pass).
*If the implementer and reviewer are the same agent identity, the merge is rejected by the system orchestrator.*

### 3.2. Data Provenance & Anti-Hallucination
*   Every functional code change must include a commit message mapped directly to a specific step in the Legislative Plan.
*   "Ghost Code" Exception: Any architectural deviation or new dependency MUST statically reference an existing Knowledge Item (KI) or an official framework doc link.

### 3.3. The Circuit Breaker & Supreme Court Deadlock Resolution
*   **The 3-Attempt Circuit Breaker (`systematic-debugging`)**: If an Executive agent fails to pass the Judicial tests 3 times, their workspace is paused. This signals a hallucination loop or flawed Legislative plan.
*   **Deadlock Resolution:** If the Executive claims the code is perfect, but the Judicial branch rejects it over a constraint, the system halts and summons the **Senior Architect**. The Architect is placed in a clean context with only the Code and the Dispute Log. Their ruling is final. If they cannot resolve it in 1 prompt, the entire task is reverted and booted to the Human.

---

## 4. "Day 2" Autonomous Operations

The machine's job is not done when the code merges. Every cycle concludes with a 360-degree Wrap-Up:
1.  **Continuous Memory Encoding**: The Judicial branch extracts the specific reason the code failed initially and commits it to `lessons_learned.md` (e.g., "Next.js 14 requires `use client` on this specific hook").
2.  **Living Documentation (`update-docs`)**: The README, C4 Architecture diagrams, and API swagger docs are automatically regenerated to reflect the new state.
3.  **Telemetry Scaling**: The system generates CLI commands (`command-expert`) required to monitor or interact with the new feature in production.

## Conclusion
By treating the LLM not as a chatbot, but as a deterministic CPU within a Zero-Trust, Three-Branch constitutional framework, we fundamentally eliminate prompt drift, regression, and hallucination. This V4 Framework is the ultimate engine for autonomous, enterprise-grade software generation.
