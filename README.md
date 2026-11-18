<h1 align="center">huh</h1>

<p align="center">
  <b>Stop guessing. Start building what you actually meant.</b>
</p>

<p align="center">
  A Claude Code skill that turns ambiguous requests into clear decisions, better implementations, and verified results.
</p>

---

AI coding agents often make assumptions when instructions aren't clear. They write code, claim it's done, and leave you to discover what they misunderstood.

`huh` changes that.

**Ask first. Build second. Verify together.**

## Results

Tested on real engineering tasks from a production codebase's development history, using the same Claude models with and without the skill.

| Metric | Without `huh` | With `huh` |
|---|---:|---:|
| **Overall success rate** | 30% | **70%** |
| Sonnet 5.5 — challenging tasks | 17% | **72%** |
| Sonnet 5.5 — new tasks | 46% | **71%** |
| Haiku 5.5 — new tasks | 25% | **67%** |
| Incorrect verification claims | 27% | **0%** |

### Key findings

- **2.3× higher success rate** across benchmark runs.
- **Zero regressions** across all three experiments.
- **Zero false verification claims** with `huh`.
- **Haiku 5.5 with `huh` outperformed Sonnet 5.5 without it** on the same tasks.
- **Statistically significant improvements** in all three experiments.

Same models. Same tasks. Better results.

## How it works

1. **Understand** — Read the request, relevant code, and existing tests.
2. **Clarify** — Identify missing decisions and ask focused questions with suggested answers.
3. **Build** — Implement based on confirmed requirements, not assumptions.
4. **Demonstrate** — Show concrete input/output examples instead of simply claiming success.
5. **Refine** — Fix what you flag, verify again, and report what's actually confirmed.

**No endless back-and-forth. No silent assumptions. No unearned "done."**

## Install

```bash
git clone https://github.com/Mikebouskila/huh ~/.claude/skills/huh
```

Then, in Claude Code:

```text
/huh <your request>
```

## When to use it

Features, bug fixes, refactoring, and engineering tasks where getting the intended behavior right matters.

Designed for interactive development with someone available to clarify requirements and review results.

## Why "huh"?

*"Huh?"* is one of the most universal expressions in human language, with remarkably similar forms across dozens of languages.

It's what humans say when something isn't clear.

AI coding agents should learn to do the same.
