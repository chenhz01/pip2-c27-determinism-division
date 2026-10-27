# PIP-2.0 · Determinism Division

**3 primitives on one question: Half the steps should be code, not tokens. Nobody asks which.**

[![License: Apache-2.0](https://img.shields.io/badge/code-Apache--2.0-blue.svg)](LICENSE) [![Spec: CC BY 4.0](https://img.shields.io/badge/spec-CC%20BY%204.0-lightgrey.svg)](LICENSE-SPEC)

---

## The problem

PIP-1.0 decided **when an iteration should stop**. This set looks one layer down — at the loop itself, at the tools it calls, and at the honesty of what it reports:

1. **The loop is sick, not slow.** It is livelocked, waiting on itself, or oscillating between two answers. Every metric still says 'working'.
2. **The tools answer, but their answers have no semantics.** Fresh? Stale? Timed out? Retryable?
3. **Nobody audits the auditor.** The judge that gates every step drifts, and the evaluation itself now costs several times what the agent costs.
4. **Conclusions are not falsifiable.** No source for the numbers, no counterexample required, no condition under which the claim would die.

`PIP-2.0` ships **3 primitives** (148 lines of Python in total). Each is **30–80 lines, standard library only, embeddable in any loop**.

It is not a framework. It is a toolbox — take the wrench you need.

---

## What is in here

| Cluster | What it protects you from | Primitives |
|---|---|---|
| **Determinism Division** | Half the steps should be code, not tokens. Nobody asks which. | 3 |
| | **total** | **3** |

<sub>Learning cards in `cards/CARDS.md` are written in Chinese (plain-language → mechanism → how to use → when it fails). Code, identifiers and this README are English.</sub>

---

## Quick start

```bash
python components/L97-determinizable-detect/impl.py      # what it does, on built-in demo data
python components/L97-determinizable-detect/selftest.py  # hard assertions that it does that
python run_all.py                 # every component, own process each
```

```python
import sys; sys.path.insert(0, 'components/L97-determinizable-detect')
from impl import *                # then call it from your own loop
```

---

## What has been verified, and what has not

| Check | Result | Note |
|---|---|---|
| Runs in its own process | **3/3** | both `selftest.py` and `impl.py`, fresh interpreter each |
| Third-party dependencies | **0** | stdlib only, by construction |
| Determinism | enforced in-repo | no network, no randomness; seeded where unavoidable |
| Explicit bad-input contract | **partial** | not every primitive validates its inputs explicitly; some rely on native exceptions. We did not add no-op guards just to satisfy a checker |
| Real-world adoption | **none yet** | these are new; no production usage is claimed |

**Honest limits.** Each primitive decides from structured data you must supply — scores, events, manifests, calls. It cannot judge whether a design is good, whether prose has a voice, or whether a judgement about people is fair. Forcing it into those questions produces confident nonsense.

---

## License and attribution

Dual-licensed:

- **Code** — Apache License 2.0. See [LICENSE](LICENSE).
- **Specification & docs** — Creative Commons Attribution 4.0 International (CC BY 4.0). See [LICENSE-SPEC](LICENSE-SPEC).

If you publicly claim that your implementation **conforms to / passes / implements PIP-2.0**, you must attribute: `PIP-2.0 · pip2-c27-determinism-division © 2026 chenhz01, CC BY 4.0` plus the spec link https://github.com/chenhz01/pip-v2-process-iteration-primitives.

If you make no such claim, use it freely — commercial, closed-source, renamed, no attribution needed.

