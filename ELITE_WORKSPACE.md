# THE ELITE WORKSPACE CONSTITUTION

This document defines the unified engineering standards for all projects in this workspace. 

## ⚖️ THE PRIME DIRECTIVE: TigerStyle (TigerBeetle)
**Safety and Correctness over all.** 
- **Determinism:** Code must be deterministic. Avoid hidden state or non-deterministic APIs.
- **Fail Fast:** If a condition is met that should never happen, the system should crash immediately (Assertions).
- **Static > Dynamic:** Prefer compile-time checks and static allocations over runtime complexity.
- **No Magic:** Avoid abstractions that obscure what is actually happening.
- **Hardware-Level Integrity:** Never rely solely on application-level validation. Enforce critical invariants (like enum ranges and required fields) at the storage layer using `CHECK` constraints and `NOT NULL` directives.

## 💾 DATA LAYER STANDARDS
- **Raw SQL + Pydantic (The "Contract" Pattern):** Avoid ORM "magic" for core business entities. Use explicit Raw SQL for data access to ensure transparency and hardware efficiency. Parse all results into Pydantic models at the repository boundary to ensure type safety.
- **Stateless Functional Repositories:** Repositories must be collections of pure functions, not classes. They should take a database connection/session as an argument and return data structures, maintaining zero internal state.
- **Integer Enums:** Store enums as integers in the database for performance, storage efficiency, and cross-language compatibility. Provide human-readable labels only at the presentation layer.

## 🧠 THE ARCHITECTURAL PHILOSOPHY: Dr. John Ousterhout & David Parnas
- **Fight Complexity:** Complexity is anything that makes it hard to understand or modify the system.
- **Deep Modules:** Interfaces should be simple; implementations can be complex but must be hidden.
- **Strategic vs. Tactical:** Invest time now to create a better design; never "hack it in" to save time.
- **The Parnasian Audit:** Every module must be subjected to the following questions *during the architectural review phase*:
    1. What design decision does this module hide? (If none, why does the module exist?)
    2. Where else is this decision assumed or duplicated? (Who else “knows” this fact?)
    3. If this decision changes, how many files must change? (One is good. Many is a design failure.)
    4. Can this feature be removed without breaking unrelated code? (Does the system shrink cleanly?)
    5. Is this module structured around change, or around execution flow? (Volatility vs pipeline thinking.)
- **Code Review:** Adhere to [Ousterhout's Review Codes](https://web.stanford.edu/~ouster/cgi-bin/cs190-spring16/reviewCodes.php).
- **Transaction Ownership (Unit of Work):** Repositories must never control transaction boundaries (e.g., calling `commit()`). They should only `flush()` changes. The ownership of the transaction (`commit`/`rollback`) belongs exclusively to the Orchestrator or Service layer to ensure atomicity across multiple side-effects.
- **Boundary Guardians:** All system boundaries (API inputs, File IO, Environment Config) must be guarded by static validation models (e.g., Pydantic). Fail fast at the edge to keep the "Deep Module" core pristine and type-safe.

## 🚀 PERFORMANCE & EFFICIENCY: Dean & Ghemawat
- **Respect the Hardware:** Follow [Abseil Efficiency Hints](https://abseil.io/fast/hints.html).
- **Minimize Allocations:** Avoid unnecessary memory churn.
- **Data over Code:** Prefer simple data structures that fit in cache.

## 🛠 THE WORKFLOW: Harper Reed, Beads & Zagi
- **One Question at a Time:** The agent must ask exactly one question to move the design forward. No guessing.
- **PRD First:** No code is written until a PRD/Spec is agreed upon. The agent is the steward of clarity.
- **Parnasian Mandatory:** The "Parnasian Audit" must be performed and documented in the PRD or Design Spec before any implementation begins.
- **PRD Lock Is Explicit:** A PRD is not considered agreed upon until the user explicitly states "PRD locked". The agent must not close PRD/Definition Beads or begin implementation without this explicit confirmation.
- **PRD Lock Requires Artifact:** The statement "PRD locked" is only valid if a PRD document exists and includes problem statement, users, non-goals, authority semantics, and success criteria.
- **Uncertainty Blocks Semantics:** If the user is unsure about a core semantic decision, the agent must not propose a specific value as a baseline; it must ask for a choice among alternatives.
- **Tracer Bullets:** Use `_spikes/` only for disposable experiments that resolve exactly one unknown blocking a PRD decision. This code is radioactive (no imports or copying to/from `src/` or `lib/`), must produce a documented PRD update, and must be deleted or archived before "PRD locked" and any clean implementation begins.
- **The Systemic Sweep:** Any task involving a cross-cutting concern (e.g., Time, Logging, Error Handling) requires a mandatory workspace-wide discovery (`grep`) before implementation. This ensures the fix is **Strategic** (system-wide) rather than **Tactical** (local).
- **Task Orchestration:** Every task must be a Bead (`bd`).
- **Git Guardrails:** Always use `zagi` for git operations. This ensures prompts are logged and commits follow strict guardrails.
- **Environment:** All Python work must use `uv`.

## 🔄 ULTRALEARNING LOOP
- After every significant task, the agent and human will perform a "Knowledge Compounding" check.
- **MANDATORY:** The results of this check must be appended to `~/projects/KNOWLEDGE_COMPOUNDING.md` with the date, project name, and the three core questions (Difficult Part, Concept Mastered, Next Application).
- This ensures cross-project learning is captured in a single source of truth.
