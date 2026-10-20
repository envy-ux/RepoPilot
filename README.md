<p align="center">
  <img src="assets/repopilot-banner.svg" alt="RepoPilot — Repository Intelligence Agent" width="430" />
</p>

<p align="center">
  <a href="https://github.com/envy-ux/RepoPilot/actions/workflows/pytest.yaml"><img src="https://github.com/envy-ux/RepoPilot/actions/workflows/pytest.yaml/badge.svg" alt="Tests"></a>
  <img src="https://img.shields.io/badge/Python-3.11%2B-3776AB" alt="Python 3.11+">
  <img src="https://img.shields.io/badge/License-MIT-green.svg" alt="MIT License">
  <img src="https://img.shields.io/badge/Status-Downstream%20fork-orange" alt="Downstream fork">
</p>

# RepoPilot — Repository Intelligence Agent

RepoPilot is a command-line AI software-engineering agent designed to investigate repository issues, make code changes, and validate proposed fixes in a controlled execution environment.

> **Important provenance note:** this initial RepoPilot distribution is a branded, downstream derivative of [SWE-agent](https://github.com/SWE-agent/SWE-agent), distributed under its MIT license. Its core agent runtime, tools, configuration system, and much of its documentation are inherited from SWE-agent. RepoPilot-specific capabilities such as AST-based repository indexing, dependency-graph retrieval, and automatic impacted-test selection are **roadmap items, not implemented features in this initial package**. See [`UPSTREAM_NOTICES.md`](UPSTREAM_NOTICES.md) and [`REPOPILOT_ROADMAP.md`](REPOPILOT_ROADMAP.md).

## What works in this initial distribution

The inherited SWE-agent runtime provides a foundation for:

- Running an LLM-driven agent against a software issue or task.
- Editing code and executing shell tools inside a configured environment.
- Configuring model and agent behavior through YAML.
- Running single tasks or batches and inspecting saved trajectories.
- Using LiteLLM-supported model providers, subject to each provider's current API and credentials.

The repository also adds the `repopilot` command alias and RepoPilot-branded project metadata. The original `sweagent` command and `sweagent` Python import namespace are retained for compatibility with the inherited code and docs.

## Quick start

### Requirements

- Python 3.11 or newer.
- Git.
- Credentials for a supported language-model provider.
- Docker is recommended for isolated execution. Review the inherited environment/deployment docs before running tasks against repositories you care about.

### Install from source

```bash
git clone https://github.com/envy-ux/RepoPilot.git
cd RepoPilot
python -m venv .venv
```

Activate the virtual environment, then install the package:

**Windows PowerShell**

```powershell
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -e ".[dev]"
repopilot --help
```

**macOS / Linux**

```bash
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -e ".[dev]"
repopilot --help
```

### Configure model credentials

Set the environment variable required by the provider you choose. For example, in PowerShell:

```powershell
$env:OPENAI_API_KEY = "your-key"
```

Or in macOS/Linux:

```bash
export OPENAI_API_KEY="your-key"
```

Do not commit real API keys or tokens. A safe starter template is provided in [`.env.example`](.env.example); keep your actual `.env` file private.

### Run a task

First inspect the command options:

```bash
repopilot run --help
```

Then follow the inherited [hello-world guide](docs/usage/hello_world.md) for the complete command syntax and environment setup. Examples in the inherited documentation may use the backwards-compatible `sweagent` command; the `repopilot` alias invokes the same CLI entry point.

## Architecture at a glance

1. **Task input** — issue description or problem statement and target repository.
2. **Agent loop** — language model reasons over observations and available tools.
3. **Execution environment** — commands run through the configured SWE-ReX backend (Docker is the usual local option).
4. **Patch and trajectory** — proposed changes and run traces are saved for inspection.
5. **Evaluation** — run the target project's tests and review the generated diff before accepting changes.

## Roadmap

RepoPilot's planned differentiators are documented separately so current functionality is not confused with future work:

- [ ] AST-based repository index using Tree-sitter.
- [ ] Symbol and file dependency graph for context retrieval.
- [ ] Git-diff-aware impacted-test selection, with an optional TestPath integration.
- [ ] Sandboxed patch verification with before/after test results.
- [ ] Benchmark suite for issue-resolution rate, test-selection recall, runtime, and model cost.
- [ ] CI quality gate and machine-readable run reports.

Contributions toward these features are welcome. Open an issue in the RepoPilot repository to discuss a proposed feature or contribution.

## Development checks

After installing the dev extras, useful checks include:

```bash
python -m compileall sweagent
python -m pytest -m "not slow"
```

The upstream test suite may require additional services, credentials, or environment-specific setup. CI results should be checked in the repository's **Actions** tab; this prepared archive has not been represented as passing the full upstream test suite.

## Documentation and attribution

The `docs/`, `config/`, `tools/`, and `sweagent/` directories retain upstream implementation and documentation in many places. For details on the original project's design and research, see [SWE-agent](https://github.com/SWE-agent/SWE-agent) and its [paper](https://arxiv.org/abs/2405.15793). This derivative does not claim the upstream implementation or research as original RepoPilot work.

## License

This distribution retains the upstream [MIT License](LICENSE). See [`UPSTREAM_NOTICES.md`](UPSTREAM_NOTICES.md) for provenance and attribution.
