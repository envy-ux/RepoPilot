# RepoPilot implementation status

This file distinguishes inherited functionality from RepoPilot-specific work still to be built.

## Available from the inherited SWE-agent base

- LLM-driven repository issue/task execution through the existing agent loop.
- Tool execution through the configured SWE-ReX environment backend.
- YAML-based agent/environment configuration.
- Single-run and batch-run commands, plus trajectory inspection utilities.
- The upstream test suite and documentation, with original `sweagent` imports and command retained.

## RepoPilot-specific additions in this prepared package

- Distribution metadata branded as `repopilot`.
- `repopilot` CLI alias that calls the inherited CLI entry point.
- RepoPilot README, repository notices, security guidance, and roadmap.
- Repository links and workflow settings prepared for a new public GitHub repository.

## Not implemented yet

These are intended differentiators, not current capabilities:

1. **Repository index:** parse source using Tree-sitter and store files, symbols, imports, and calls.
2. **Dependency graph:** link symbols and tests to their dependencies; update only affected nodes after a diff.
3. **Impact-based test selection:** select likely relevant tests from changed files and dependency paths, with a safe fallback to the full suite when confidence is low.
4. **Patch verification:** apply changes in an isolated worktree/container, run selected tests, then run the full suite before marking a patch verified.
5. **Evaluation:** publish reproducible benchmark data for patch success, test-selection recall, false negatives, runtime, and token/API cost.

The safety principle for test selection is important: optimized test selection must be measured against full-suite runs, and uncertain changes should trigger a full test run rather than silently skipping relevant tests.
