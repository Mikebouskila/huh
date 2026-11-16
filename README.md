# huh

> **huh?** What you say when something is not clear. Linguists have found a near-identical word in dozens of languages.

A Claude Code skill that asks before it builds. When a request leaves a decision open, most agents guess and tell you afterwards. `huh` lists the open decisions, asks you once, builds to your answers, and shows you concrete results until you have no corrections.

Made by Pomela.

## Results

Real Claude Code runs on real engineering tasks from Pomela's own commit history, graded by hidden tests the agent never saw. Each test compared the same model with and without the skill.

| Test | Without | With `huh` |
|---|---|---|
| 9 tasks Sonnet 5.5 had failed before (2 runs each) | 3/18 (17%) | **13/18 (72%)** |
| 24 new tasks, Sonnet 5.5 | 11/24 (46%) | **17/24 (71%)** |
| The same 24 tasks, Haiku 5.5 | 6/24 (25%) | **16/24 (67%)** |

- **No task got worse.** Across the three tests, 22 tasks improved and 0 regressed.
- **A "done" you can trust.** Wrong "verified" claims: 0 of 66 runs with `huh`, 18 of 66 without.
- **Statistically significant in all three tests** (exact one-sided p = 0.016, 0.016 and 0.001, with the task as the unit).
- **A smaller model catches up.** Haiku 5.5 with `huh` passed 16/24; Sonnet 5.5 without it passed 11/24. This is an observation across two tests, not a planned comparison.

### How it was measured

- **Same conditions for both sides.** With and without the skill, the agent had the same way to ask the request's owner questions. The difference is what `huh` makes the agent do with it: without the skill, Haiku asked in 5 of 24 runs; with it, in 24 of 24.
- **The owner was simulated.** A model holding the real commit answered the agent's questions under fixed rules: only what was asked, a line or two, no code.
- **Decided in advance.** The tasks, the statistics and the pass criterion for each test were written down before the runs, and the skill text was frozen.
- **Scope.** Measured on Sonnet 5.5 and Haiku 5.5, on tasks from one codebase.

## How it works

1. **Read first.** The request, the files it names, their tests, and the nearest similar code.
2. **List the open decisions**: names and interfaces, exact outputs, edge cases, scope. Each with a best guess.
3. **Ask once, before writing code.** Numbered, one line each, with the guess so you can answer "yes".
4. **Build to the answers.**
5. **Show the result and confirm.** 6-10 concrete input and output lines; you mark what is wrong; it fixes and repeats until you have no corrections.
6. **Report** what you confirmed and what is still a guess.

Expect about three short messages per task.

## Install

```bash
git clone https://github.com/Mikebouskila/huh ~/.claude/skills/huh
```

Then, in Claude Code:

```
/huh <your request>
```

## When to use it

Use it for features and bug fixes when someone who knows the intent is there to answer. It is built for working sessions with a person; skip it for one-line edits and for unattended runs where nobody can answer.
