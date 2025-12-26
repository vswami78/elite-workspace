# THE ELITE WORKSPACE CONSTITUTION

This document defines the unified engineering standards for all projects in this workspace. 

## ⚖️ THE PRIME DIRECTIVE: TigerStyle (TigerBeetle)
**Safety and Correctness over all.** 
- **Determinism:** Code must be deterministic. Avoid hidden state or non-deterministic APIs.
- **Fail Fast:** If a condition is met that should never happen, the system should crash immediately (Assertions).
- **Static > Dynamic:** Prefer compile-time checks and static allocations over runtime complexity.
- **No Magic:** Avoid abstractions that obscure what is actually happening.

## 🧠 THE ARCHITECTURAL PHILOSOPHY: Dr. John Ousterhout
- **Fight Complexity:** Complexity is anything that makes it hard to understand or modify the system.
- **Deep Modules:** Interfaces should be simple; implementations can be complex but must be hidden.
- **Strategic vs. Tactical:** Invest time now to create a better design; never "hack it in" to save time.
- **Code Review:** Adhere to [Ousterhout's Review Codes](https://web.stanford.edu/~ouster/cgi-bin/cs190-spring16/reviewCodes.php).

## 🚀 PERFORMANCE & EFFICIENCY: Dean & Ghemawat
- **Respect the Hardware:** Follow [Abseil Efficiency Hints](https://abseil.io/fast/hints.html).
- **Minimize Allocations:** Avoid unnecessary memory churn.
- **Data over Code:** Prefer simple data structures that fit in cache.

## 🛠 THE WORKFLOW: Harper Reed, Beads & Zagi
- **One Question at a Time:** The agent must ask exactly one question to move the design forward. No guessing.
- **PRD First:** No code is written until a PRD/Spec is agreed upon. The agent is the steward of clarity; even if the user says "Go ahead and implement," the agent must continue questioning if any part of the specification remains fuzzy or non-deterministic.
- **PRD Lock Is Explicit:** A PRD is not considered agreed upon until the user explicitly states "PRD locked". The agent must not close PRD/Definition Beads or begin implementation without this explicit confirmation.
- **PRD Lock Requires Artifact:** The statement "PRD locked" is only valid if a PRD document exists and includes problem statement, users, non-goals, authority semantics, and success criteria.
- **Uncertainty Blocks Semantics:** If the user is unsure about a core semantic decision, the agent must not propose a specific value as a baseline; it must ask for a choice among alternatives.
- **Tracer Bullets:** Use `_spikes/` only for disposable experiments that resolve exactly one unknown blocking a PRD decision. This code is radioactive (no imports or copying to/from `src/` or `lib/`), must produce a documented PRD update, and must be deleted or archived before "PRD locked" and any clean implementation begins.
- **Task Orchestration:** Every task must be a Bead (`bd`).
- **Git Guardrails:** Always use `zagi` for git operations. This ensures prompts are logged and commits follow strict guardrails.
- **Environment:** All Python work must use `uv`.

## 🔄 ULTRALEARNING LOOP
- After every significant task, the agent and human will perform a "Knowledge Compounding" check.
- **MANDATORY:** The results of this check must be appended to `~/projects/KNOWLEDGE_COMPOUNDING.md` with the date, project name, and the three core questions (Difficult Part, Concept Mastered, Next Application).
- This ensures cross-project learning is captured in a single source of truth.
