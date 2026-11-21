# [PROJECT] — Project Rules

*The standing brief, read by the agent every session. Limit: [8] KB (rule 11).*

## About the owner

- **Not a coder.** The owner says what they want in plain English; the agent implements it.
- **The owner decides taste, the agent the technical.** The owner's: [how it looks, sounds and reads; the words it uses], privacy, money, and reversing any decision of theirs. The agent's: how a thing is built, which test, a trial's settings, tidy-ups; each one line at the wrap, the owner's to overturn. Explain a taste trade-off and wait; record reasons in the decisions file or the log.
- **The decision round.** A session opens with one short message: **three decisions at most**, often none, no code. One that appears mid-build is put then; the agent carries on with what doesn't depend on it. It reads the last [10] log entries' Friction lines; one seen three times becomes a decision, with "is it worth it?".
- **The owner's eye and ear are the gate.** Keep the approved version as the default until the owner has seen or heard the proposed change to [feel: look, voice, wording] and made the call. Put a plainly named before/after pair in `[REVIEW_FOLDER]`. At most three wait there at once.
- **Short in chat.** A table beats a paragraph; one line at every milestone.
- **Spending.** Every paid test run is asked first, with the count and the cost; there is no standing yes. Tests use a cheaper model wherever one can stand in.
- **Is it worth it?** Every test, fix or proposal says what it means in daily use (how often, what the owner would see or hear), with an honest call. "Leave it" or "can you live with it?" is always a real option.
- **Outside eyes.** If used, follow `docs/outside-reviews.md` before paying to try a design and after a surprising result. One reviewer per question, a second only before money is spent or something hard to undo; never a review of a review. Which model does what is written here and nowhere else: [e.g. model A for wide views, model B to critique plans; any design model]. A design model drafts in its own folder; the agent copies each approved handoff into the repo the day it wires it.

## What this is

[One paragraph: what the project does, its main files, what it runs on, the machine it runs on.]

## What to read

| Document | When |
|---|---|
| `docs/PROGRESS.md` | Every session: where we are, next, queued, waiting for the owner. |
| `docs/settled.md` | If used, at the round: what is true today, by area. |
| `docs/decisions.md` | If used, at the wrap and for a settled line's reason. Otherwise use the log's Decisions line. |
| `docs/log/YYYY-MM.md` | At recovery, for recent Friction lines, and for the current session entry. |
| `README.md` | How to run it. Kept true; not a changelog. |

**A session's shape:** read PROGRESS → crash check → decision round → start the log entry → build → checks → the pair for the owner → wrap the docs → commit. Sessions are named `S[n] — [what it advances]`.

**Crash check:** before the decision round, compare recent commits and staged, unstaged and new files with the last log entry. After an interruption, reconcile the log and PROGRESS from evidence you can verify. Leave unexplained changes in place and label them unverified. Take owner approval from an explicit record or ask again if it matters to the next step.

## Project rules

*Fill the brackets in rules 1 and 5 for your project alone; the rest is the workflow, so keep it.*

1. **[The medium rule.]** [e.g. Everything it writes is read aloud: a change that reads better but sounds worse is out.]
2. **One variable at a time.** Trials hold everything fixed but the one thing changed; the exact scope the owner approved is recorded, never widened.
3. **One writer in the project at a time.** That includes code and shared workflow files. A second session may read, research or draw in its own folder.
4. **Nothing is undone silently.** Record a reversal with the earlier decision's ID or session and the reason. Use a temporary switch when trying both versions helps. Record its decide-by date in `settled.md` (or PROGRESS, with the core files only). Raise overdue switches in the round; a change in daily use with no complaint by then is settled. Once the owner chooses, queue switch removal for the next session, after filing the old way's settings, assets and a runnable copy. Before a hard-to-undo change to saved data, record how to restore it and verify the backup.
5. **Behaviour lives in [prompt/config files],** code handles delivery. [What belongs where.] A change to what the model is handed (memory, context) is checked against the whole prompt for contradictions.
6. **The owner's private material stays out of the repo** (`[PRIVATE_FOLDER]`); agents open it only for a task that needs it; tests use invented details. Agents never read a secrets file whole, and check other tools' snapshots for private files. If private material is tracked, pause and tell the owner without copying its contents. Revoke or rotate exposed credentials promptly.

## The working rules

7. **Quality wins.** Fix a limitation or record it in `docs/PROGRESS.md`.
8. **Surgical edits.** No code file is rewritten whole; a section at a time, the diff read before the commit.
9. **Test what the change could affect,** by name, before committing. A pass counts only from a run in this session whose output shows how many tests ran; never from memory or a summary. Log what wasn't run. Widen checks for shared code, settings, data formats and releases; before a release, also try the main user task. Never loosen a test just to get green. If the intended behaviour changes, record why and update the test to check it.
10. **Every file explains itself.** A short note at the top: purpose, inputs, outputs and reason. Not for files that can't hold one (JSON, data).
11. **Sizes are measured every session.** This file [8] KB; `PROGRESS.md` [30] KB; `settled.md` [12] KB; a log entry [10] lines; a decision row [3] lines; a function [60] lines. A limit is moved only by the owner. When a file nears its limit, nothing is deleted: older rows move word for word to their own file in `docs/`, leaving a one-line pointer, never into another file with a limit.
12. **One documents round a session, at the wrap.** Before building, start the log entry with the session ID, scope, starting commit and any opening approvals. Record later approvals there when given. Save checked steps in scoped commits. Finish the log and update the other docs at the wrap. What the session did goes in the log; PROGRESS keeps only what is still open. **A small session** (nothing the owner would see or hear, no new switch or reversal, at most [50] changed lines of code; if in doubt, it isn't small) writes a log entry marked *small* and its decision rows. PROGRESS, settled and limitations change only if one of their lines did; sizes are measured only for the files it touched. Any log entry may end with one **Friction** line: what in the workflow felt heavy, slow or confusing. Preserve a recoverable copy of work before any operation that could discard it, including work Git doesn't track. History rewrites require the owner's explicit approval and a coordinated sensitive-data cleanup plan.
13. **Ideas go in PROGRESS** with why not now.
14. **Deleting files needs a list,** checked file by file against the backup (`[BACKUP_LOCATION]`; git, for files it tracks). Never a count.
15. **A new place retires an old one.** A new folder, file or routine says which old one it replaces, and that one is retired in the same session. Each fact has one home too: other files point to it, and a number that keeps changing (a count, a size) comes from a script's output, not a copy.
16. **Evidence in three kinds, kept apart:** our tests, someone's view, published work. Citations are marked verified or not.
17. **Agree on paper how results are judged before comparing.** The current way is always an option; "change nothing" is valid.
