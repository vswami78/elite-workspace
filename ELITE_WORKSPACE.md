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
- **PRD First:** No code is written until a PRD/Spec is agreed upon.
- **Task Orchestration:** Every task must be a Bead (`bd`).
- **Git Guardrails:** Always use `zagi` for git operations. This ensures prompts are logged and commits follow strict guardrails.
- **Environment:** All Python work must use `uv`.

## 🔄 ULTRALEARNING LOOP
- After every significant task, the agent and human will perform a "Knowledge Compounding" check:
  1. What was the most difficult part?
  2. What concept was mastered?
  3. How do we apply this to the next bead?
