# [PROJECT] — Project Rules

*The standing brief, read by the agent every session. Limit: [8] KB (rule 11).*

## About the owner

- **Not a coder.** The owner says what they want in plain English; the agent implements it.
- **The owner decides taste, the agent the technical.** The owner's: [how it looks, sounds and reads; the words it uses], privacy, money past the standing budget, and reversing any decision of theirs. The agent's: how a thing is built, which test, a trial's settings, tidy-ups; each one line at the wrap, the owner's to overturn. Explain a taste trade-off and wait; record reasons in `docs/decisions.md`.
- **The decision round.** A session opens with one short message: **three decisions at most**, often none, no code. One that appears mid-build is put then; the agent carries on with what doesn't depend on it.
- **The owner's eye and ear are the gate.** A change to [feel: look, voice, wording] is done when the owner has seen or heard it and said what they felt. No review pages: a before/after pair in `[REVIEW_FOLDER]`, named plainly. At most three wait there at once.
- **Short in chat.** A table beats a paragraph; one line at every milestone.
- **Budget.** A standing yes for test runs up to [$/run] a run and [$/week] a week; past either, state the count and cost and wait.
- **Outside eyes.** The agent coordinates. Models from other labs challenge before money is spent on a design and after a surprising result, by a short brief the owner pastes (`docs/outside-reviews.md`). Every reply is checked against the code before anything follows.

## What this is

[One paragraph: what the project does, its main files, what it runs on, the machine it runs on.]

## What to read

| Document | When |
|---|---|
| `docs/PROGRESS.md` | Every session: where we are, next, queued, waiting for the owner. |
| `docs/settled.md` | At the round: what is true today, by area. |
| `docs/decisions.md` | At the wrap, to add rows; for the reason behind a settled line. |
| `docs/log/YYYY-MM.md` | Only for detail on a past session. |
| `README.md` | How to run it. Kept true; not a changelog. |

**A session's shape:** read PROGRESS → crash check → decision round → build → checks → the pair for the owner → log, PROGRESS, decisions, settled, sizes → commit. Sessions are named `S[n] — [what it advances]`.

**Crash check:** before the decision round, compare recent commits and any uncommitted or new files with the last log entry. If an earlier session ended mid-build before its wrap (a usage limit, a crash), bring `PROGRESS.md` and the log up to date from them and its closing message first; mark what can't be confirmed as unverified.

## Project rules

*Rules 1 and 5 are yours to write: fill the brackets with what is true of your project alone. Rules 2, 3, 4 and 6 are part of the workflow; keep them.*

1. **[The medium rule.]** [e.g. Everything it writes is read aloud: a change that reads better but sounds worse is out.]
2. **One variable at a time.** Trials hold everything fixed but the one thing changed; the exact scope the owner approved is recorded, never widened.
3. **One writer in the code at a time.** A second session may read, research or draw, never edit the code.
4. **Nothing is undone silently.** A change that reverses an earlier session's work is a decision row that names the old one and says why. The old way stays behind a switch until the owner has tried both.
5. **Behaviour lives in [prompt/config files],** code handles delivery. [What belongs where.]
6. **The owner's private material stays out of the repo** (`[PRIVATE_FOLDER]`); agents open it only for a task that needs it; tests use invented details. A secret in a diff stops work until it is rotated.

## The working rules

7. **Quality wins.** Fix a limitation or record it in `docs/PROGRESS.md`.
8. **Surgical edits.** No code file is rewritten whole; a section at a time, the diff read before the commit.
9. **Test what the change could affect,** by name, before committing. A pass counts only from a run in this session whose output shows how many tests ran; never from memory or a summary. Log what wasn't run. Never loosen a test to pass.
10. **Every file explains itself.** A short note at the top: purpose, inputs, outputs and reason.
11. **Sizes are measured every session.** This file [8] KB; `PROGRESS.md` [30] KB; a log entry [10] lines; a decision row [3] lines; a function [60] lines. A limit is moved only by the owner. When `PROGRESS.md` nears its limit, nothing is deleted: older rows move word for word to their own file in `docs/`, leaving a one-line pointer; `settled.md` stays a short summary.
12. **One documents round a session, at the wrap.** Code may be committed in steps with one-line messages; the log, decisions, settled and PROGRESS are written once, at the end. No history-rewriting git.
13. **Ideas go in PROGRESS** with why not now.
14. **Deleting files needs a list,** checked file by file against the backup. Never a count.

## The log entry

```
### S[n] — [title] ([date])
[One or two sentences: scope.]
**What changed.** [files and numbers]
**Checks.** [tests run; "not run, no change to X" for the rest]
**Sizes.** [this file, PROGRESS.md, this entry, the longest function touched]
**The review.** [the pair's name and what the owner said, or "waiting"]
**Decisions.** [one line each; reversals name the old row]
**Deferred.**
```
