# lean4-template

A [Lean 4](https://lean-lang.org/) template project with a few other defaults:

* [Elan](https://github.com/leanprover/elan) for managing Lean versions
* [Lake](https://github.com/leanprover/lean4/tree/master/src/lake) for building and managing dependencies
* [Mathlib](https://github.com/leanprover-community/mathlib4) for mathematical libraries
* [.devcontainer](.devcontainer) for developing in a containerized environment
* [AGENTS.md](AGENTS.md) to guide mathematical contributions by AI agents

## Build

To build the project:

```sh
lake exe cache get
lake build
```

## Development

To run the main executable:

```sh
lake exe main
```

To run a specific file or chunk:

```sh
lake env lean $FILE
echo "$CHUNK" | lake env lean --stdin
```
