---
name: huh
description: Before building from a request, find the decisions it leaves open (names, interfaces, exact outputs, edge cases, scope), ask the person who owns the request about them in one batch, then build to the answers and report what is confirmed and what is still a guess. Use for implementation and bug-fix requests when someone who knows the intent can answer questions. Not needed for one-line edits or fully specified tasks.
---

# Ask, then build

Most wrong "done" reports come from a decision the request left open and the builder guessed. Do not guess what the owner can tell you in one line.

## 1. Read first
Read the request, every file it names, the tests for that area, and the code that already handles the nearest similar case. Do not ask what the repo answers.

## 2. List the open decisions
Write `.rf/open.md`: one numbered line for each decision that a reviewer, or a test written by the owner, could depend on and that neither the request nor the repo fixes. Go through these four kinds in order:

- **Interface:** names of new functions, exports, files, fields and options; their arguments and return shape; where they live.
- **Exact outputs:** strings, messages, error codes, ids, ordering and formats that a caller or a test would compare.
- **Cases:** what must happen at each edge the request implies but does not spell out (empty, missing, already done, the other role or state, a limit).
- **Scope:** which neighbouring behaviours must change with this one and which must stay as they are. For each rule the existing code applies to a similar case, whether it applies here too.

Add your best guess to each line and what it is based on. Keep the list to the decisions that matter most (about 12 at most).

## 3. Ask once, before writing code
Send the list to the owner in one message: numbered, each question answerable in one line, each with your guess so they can reply "yes". Always include this question: "Which public names must exist when I am done (every export, function, file, field and option), with their arguments and return shape? My list so far is: ... Is anything missing or named differently?" The owner often has names in mind that you would not think to ask about. Ask with AskUserQuestion, or with the channel the request names. If nobody can be asked, keep your guesses and go on.

## 4. Build to the answers
Write each answer next to its line in `.rf/open.md`. Implement exactly what was confirmed, including the names. Test each confirmed line, and run tests with a time limit.

## 5. Show the result and confirm, until there are no corrections
When the code works, send the owner what it does now as a numbered list they can mark line by line:

- 6 to 10 concrete examples, one per line: a real call with its input and the output you observed. Include at least one per rule and one per edge case.
- The final public names, one per line, with arguments and the fields of what they return.

Ask: "Mark each line right or wrong, and give the right result for the wrong ones." Fix everything they correct and run the tests again. Then send the corrected lines once more, together with new examples for any case their corrections revealed. Repeat until a reply has no corrections, or the owner stops answering.

## 6. Report
Say what the owner confirmed, and list every decision that is still your own guess. Then exactly one status:

- **VERIFIED**: the tests pass, the owner's last reply had no corrections, and no decision that matters is still a guess.
- **PARTIAL**: something is unbuilt, failing, or built on a guess the owner did not confirm. List it.
- **BLOCKED**: a required step needs something you do not have. Name it.
- **FAILED**: say what was tried.
