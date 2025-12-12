---
description: "Reduce the risk of doc rot, i.e. current truths become future lies"
alwaysApply: true
---

# Pinocchio Rule (Avoid Text That Could Become Lies)

The Pinocchio Rule is a locality rule for all prose in a codebase — comments, READMEs, docs, wikis, design notes. **Avoid text that could become lies.**

Scope: Pinocchio is only about documentation. It constrains what you write about code, not how you structure or name code itself.

Extra detail can feel helpful in the moment, but every non‑local statement adds a growing risk of drift. As surrounding code evolves, far‑away prose silently turns into falsehood. Pinocchio keeps documentation trustworthy by keeping it local, stable, and minimal.

## Pragmatics and rule interactions

Other rules or ecosystem standards can create documentation requirements that Pinocchio cannot satisfy perfectly. For example, some codebases require docstrings that reference argument names or include type information. That repeats signature‑controlled details and is, strictly speaking, a Pinocchio violation.

In those situations, Pinocchio is about choosing the path least likely to result in lies:

- Include only what the standard requires; avoid extra restatement.
- Prefer mechanically‑derived or tool‑checked docs (generated stubs, typed doc tools) so refactors update prose along with code.
- Still avoid repeating defaults, exact values, or behavior summaries beyond the mandated surface.

## Guidelines

- Don’t restate behavior that the code already expresses. If the code is the source of truth, prose should not duplicate it.
- Don’t encode code‑controlled specifics in prose (defaults, exact values, schemas, return shapes). Let signatures, constants, and tests be the authority.
- Keep documentation **local** to the unit it sits next to. Describe only what is stable and directly owned by that unit.
- Don’t describe or reference non‑local details in prose (file paths, symbol names, module locations). Those will drift when code moves or is renamed.
- If cross‑cutting context is necessary, describe it at a stable conceptual level (role, boundary, invariant), not by naming where it lives.
- Prefer explaining **why** a decision exists, constraints, tradeoffs, or intent that is not inferable from code.
- If a comment/doc can go out of sync, delete it or replace it with an enforced invariant in code or tests.

## Examples

Not allowed (non‑local names/paths):

```text
# In README.md
Requests are validated in src/api/validators.py and errors are formatted in src/api/errors.py.
```

Preferred (stable conceptual truth):

```text
# In README.md
Requests are validated at the API boundary; error formatting is handled by the API layer.
```

Not allowed (duplicating code):

```py
def retry(n: int) -> None:
    # Retries 3 times with exponential backoff.
    ...
```

Preferred (why/intent only):

```py
def retry(n: int) -> None:
    # Backoff is tuned for API rate limits.
    ...
```

Not allowed (duplicating defaults):

```py
def fetch_items(limit: int = 8):
    """Fetch up to 8 items from the server."""
    ...
```

Preferred (reference the signature):

```py
def fetch_items(limit: int = 8):
    """Fetch up to `limit` items from the server."""
    ...
```
