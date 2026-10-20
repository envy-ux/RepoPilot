# Contributing to RepoPilot

Thanks for your interest in improving RepoPilot.

## Before opening a pull request

1. Search existing issues and open a focused issue for larger changes.
2. For bug fixes, include steps to reproduce and the expected behavior.
3. Add or update tests where practical and document changes to user-facing behavior.
4. Never commit API keys, GitHub tokens, private repository data, or execution artifacts.
5. Preserve upstream copyright and license notices in inherited files.

## Local checks

```bash
python -m pip install -e ".[dev]"
python -m compileall sweagent
python -m pytest -m "not slow"
```

Some inherited tests may need additional services, credentials, or environment setup. Explain any tests you could not run in the pull request.

## Upstream relationship

RepoPilot is a downstream derivative of [SWE-agent](https://github.com/SWE-agent/SWE-agent). Please keep changes scoped, identify inherited versus new behavior clearly, and retain applicable license notices. See [`UPSTREAM_NOTICES.md`](UPSTREAM_NOTICES.md).
