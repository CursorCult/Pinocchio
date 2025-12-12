# Pinocchio

The Pinocchio Rule: avoid text that could become lies by keeping documentation local, minimal, and authoritative.

Scope: this rule is only about documentation/prose.

**Install**

```sh
pipx install cursorcult
cursorcult link Pinocchio
```

Rule file format reference: https://cursor.com/docs/context/rules#rulemd-file-format

**When to use**

- You’ve seen comments or docs drift out of sync with code.
- You want documentation to stay trustworthy over time.
- You want to reduce “remote knowledge” embedded in prose.

**What it enforces**

- Prose doesn’t duplicate code, defaults, or describe non‑local details.
- Documentation stays scoped to what its enclosing unit owns.
- Cross‑cutting context stays conceptual (no symbol names/paths).
- If other standards force some duplication (e.g., parameter names in docstrings), minimize it and prefer tooling that keeps prose in sync.

**Credits**

- Developed by Will Wieselquist. Anyone can use it.
