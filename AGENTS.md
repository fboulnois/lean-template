# Agent Guidelines

## 1. Core Objectives

* **Goal:** Rigorously prove or disprove the target statement.
* **Solvability:** Assume all theorems are solvable within the current context. Never assume a problem is an "open problem" or impossible.

## 2. Environment Restrictions

* **Immutable Files:** Never modify `lakefile.toml` or `lean-toolchain`.
* **No Rebuilds:** Never run `lake clean`.
* **No External Tools:** All logic MUST remain within Lean. Do not use Python, Bash, or any external scripting tools.
* **Dependencies:** Use Mathlib as much as possible. Otherwise, prioritize existing lemmas and structures before introducing new ones.

## 3. Proving Workflow

Strictly follow this sequence for new proofs:

1. **Incremental Scope:** Advance strictly one small lemma or theorem at a time. Do not attempt monolithic proofs.
2. **Isolate:** Create a dedicated file in the `test/` directory. Include the exact `import` statements required by the target code.
3. **Iterate:** Attempt the proof in this isolated file. Follow the refactoring protocol below to optimize the proof.
4. **Divide & Conquer:** If stuck or if there are errors, immediately extract the problematic section into a separate test file and go back to step 2.
5. **Verify:**
    * Run `lake env lean <filename>`. The output MUST have **zero errors**.
    * Ensure no `sorry` or `admit` tactics remain.
6. **Integrate:** Once verified, move the code without changes into the main project source. You MUST verify that the project compiles using `lake build` after *every* step or modification.

## 4. Refactoring Protocol

1. **Optimize Proofs:** Do not guess Mathlib lemma names. Search or use `exact?` or `apply?` to discover relevant lemmas, or replace manual proofs with robust automation (`aesop`, `omega`, `linarith`, `ring`, `positivity`). Keep proofs as short as possible.
2. **Scope:** Refactor in-place. Do not migrate declarations to other files.
3. **Formatting:** Maintain idiomatic Lean 4 style. Do not exceed 100 characters per line. Never condense distinct statements onto a single line.
4. **Metrics:** Explicitly report the line count of the target file before and after refactoring.

## 5. Mathematical Docstrings

Every key lemma, theorem, or definition MUST have a Lean docstring (`/-- ... -/`) placed immediately above it. The docstring MUST include:

1. **Title:** A clear title (e.g., `**Lemma 4.1 (Valuation of Sum).**`).
2. **Description:** A concise plain text description (1-2 lines).
3. **Statement:** The formal LaTeX-formatted statement using `$$ ... $$` to display equations.
