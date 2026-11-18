# A bare-bones workflow for building with AI agents when you don't code

*What this folder is: a small set of plain-text files that let one person who doesn't code run a long software project with an AI coding agent, and bring in models from other labs as challengers. Copy the `template/` folder's files into your project, fill the `[placeholders]`, and the agent reads them at the start of every session. Nothing here depends on one tool or one lab.*

## The idea in one paragraph

AI agents forget everything between sessions, agree too easily, and will happily undo last week's work if nobody stops them. So the project's memory lives in a few files the agent must read and keep, the owner makes the calls only a human can make (taste), the agent makes and records the technical ones, and outside models are asked to argue before money is spent and after anything surprising. Results are judged by the owner looking and listening, not by reading reports.

## Who does what

| Who | Decides | Never |
|---|---|---|
| **The owner** (not a coder) | Goals, priorities and taste: what gets built and in what order; how it looks, sounds, feels and reads; privacy; money; reversing any decision of theirs | Has to read code, review pages or long reports |
| **The coding agent** (one at a time) | Technical: how a thing is built, which test, trial settings, tidy-ups. Each one recorded in a line the owner can overturn | Reverses an owner's decision silently, or guesses at taste |
| **Outside reviewers** (models from other labs) | Nothing. They challenge, draft and point out what was missed | See private material, or have a reply acted on before it is checked against the code |
| **A design model** (optional) | Drafts art or studies in its own folder | Edits the code. The agent copies each approved handoff into the repo the day it wires it, and checks it |

## The files

All six are in `template/`, laid out as they sit in your project. Every placeholder is in `[square brackets]`.

![What's in this repo: README, scars, LICENSE, and the template folder holding CLAUDE.md and docs](repo-layout.png)

| File | What it holds | Read |
|---|---|---|
| `CLAUDE.md` (or your agent's equivalent) | The standing rules. Short, with a size limit | Automatically, every session |
| `docs/PROGRESS.md` | Where we are, next, queued (with why not now), waiting for the owner, known limitations | Start of every session |
| `docs/decisions.md` | One row per decision, with the reason and whose it was. Never rewritten | At the decision round and the wrap |
| `docs/settled.md` | What is true today, by area, in one read, pointing at the rows | At the decision round |
| `docs/log/YYYY-MM.md` | One short entry per session | Only for detail on a past session |
| `docs/outside-reviews.md` | How to brief another lab's model, and the index of notes between models | When a review is due |

Also here, outside `template/`: `scars.md`, the failures behind each rule.

## A session's shape

1. **Read** `PROGRESS.md` (and `settled.md`). **Crash check:** if the last session ended mid-build (a usage limit, a crash) before writing its documents, bring them up to date from its commits and any uncommitted or new files first, and mark what can't be confirmed.
2. **The decision round:** one short message from the agent with at most three decisions for the owner, often none, and no code yet. A decision that turns up mid-build is asked then; the agent carries on with what doesn't depend on it.
3. **Build**, in small surgical edits.
4. **Check:** run the tests for what the change could affect, by name.
5. **Hand the owner something to see or hear:** a before/after pair in a folder, plainly named. Not a review page.
6. **One documents round, at the end:** the log entry, `PROGRESS.md`, new decision rows, `settled.md`, file sizes measured.
7. **Commit.** Sessions are numbered (`S1`, `S2`...) and named for what they advance.

## The rules, and why each exists

- **The owner decides taste; the agent decides the technical, and writes it down.** The owner shouldn't be asked about test settings, and the agent shouldn't guess what "feels right". Recording the agent's calls keeps them overturnable.
- **At most three decisions in the opening round.** More than three and the owner skims; fewer, better-framed choices get real answers.
- **One writer in the code at a time.** Two agents editing at once undo each other without either noticing. Others may read, research or draw.
- **Nothing is undone silently.** A reversal gets its own decision row naming the old one and why, and the old way stays behind a switch until the owner has tried both. This is the rule that stops drift.
- **Surgical edits.** No file rewritten whole; a section at a time, the diff read before the commit. Whole rewrites lose things nobody notices for weeks.
- **Test what the change could affect.** Full suites can be slow or heavy on a home machine; targeted tests run every time instead of being skipped. What wasn't run is logged. A pass counts only from a run in the same session whose output shows how many tests ran, never from memory: a run that tests nothing can still finish "green".
- **Never loosen a test to make it pass.** A green check that lies is worse than a red one.
- **Size limits on the docs.** Files the agent reads every session have a cap. Without one they bloat until the agent skims them, and the important line is the one it skips. At the limit, nothing is deleted: older lines move word for word to their own file, leaving a pointer, so `settled.md` can stay a short summary of what's true now.
- **Every file says what it is** in a short note at the top: purpose, inputs, outputs, why. A fresh agent (or you, in six months) needs no tour.
- **Ideas go in PROGRESS with why not now.** Nothing is lost, and nothing sneaks in.
- **The eye and ear are the gate.** For anything about feel, the change is done when the owner has seen or heard it and said what they felt. Agents are bad judges of taste and good at sounding sure.
- **A queue limit for the owner.** At most three things wait for the owner to look at or hear; nothing new is added until one is judged.
- **Ask before every paid run.** The agent states the count and the cost and waits for a yes; tests use a cheaper model wherever one can stand in. A standing yes under a small amount was tried, and lasted a day: the test runs that day cost more than eight times the real use.
- **Is it worth it?** Every test, fix or proposal comes with what it means in daily use and an honest call, and "can you live with it?" is always a real option. Many sessions in, the owner loses track of what a test is for; this is the line that lets them drop the ones that don't matter.
- **Private stays private.** The owner's personal material lives outside the repository; agents open it only for a task that needs it; tests use invented details.
- **Deleting files needs a list, not a count.** A clear-out goes file by file, each checked against the backup first. A count can be right while the wrong files go.
- **Limitations are written, not hidden.** What is known and not fixed goes in a list the next session reads.
- **A new place retires an old one.** A new folder, file or routine says what it replaces, and the old one goes in the same session. Otherwise notes end up waiting in a dozen places and nobody knows which is current.

## Outside reviews, in short

Before money is spent on a design, and after a result that surprised anyone, the agent writes a short self-contained brief, renamed and with counts only, that the owner pastes into a model from another lab. One reviewer per question, never a review of a review. A fresh agent that didn't write the brief reads it before it goes, and a sent brief is never changed. Models with no memory get a pasted baseline first, then "what happened since". Briefs go out from one folder and replies come back to one other; notes between models are listed in one shared index. Every reply is checked claim by claim against the real code before anything follows from it. Full method and templates: `template/docs/outside-reviews.md`.

## Quick start (copy-paste into your agent)

1. **Get the files:** on this repo's GitHub page, press the green **Code** button, then **Download ZIP**, and unzip it.
2. **Put them in your project:**
   - *A brand-new project:* copy everything inside `template/` into the new project's folder, keeping `docs/` as it is. Then use Option A.
   - *An existing project:* copy the whole `template/` folder into your project as it is, so nothing of yours is overwritten. Then use Option B.
3. **Open your agent in the project folder and paste one of these.** Not using Claude Code? Rename `CLAUDE.md` to the file your agent reads at startup (for example `AGENTS.md`).

**Option A: a brand-new project**

> Read `CLAUDE.md` and every file in `docs/`: they are templates for a workflow I want to run with you. Interview me in plain English, three questions at a time, to fill in every `[placeholder]`; keep any number already in brackets, like the size limits, unless I ask to change it. If this folder isn't a git repository yet, set one up and make the first commit. Rename `docs/log/YYYY-MM.md` to the current month, remove the invented examples, start a short `README.md` for the project, and set up `docs/PROGRESS.md`.

**Option B: an existing project**

> Read every file in the `template/` folder: it is a workflow I want to run with you. If this folder isn't a git repository yet, set one up and commit what's here before changing anything. Look through my project to draft the "What this is" section of `CLAUDE.md` and "Where we are" in `docs/PROGRESS.md`. Then interview me in plain English, three questions at a time, to fill in the remaining `[placeholders]`; keep any number already in brackets, like the size limits, unless I ask to change it. Where I already have a `CLAUDE.md`, `README.md` or `docs/` file, merge into it and never overwrite what's mine. Move the files into place, remove the invented examples and the `template/` folder, and open our first session with the decision round.

## Honest caveats

Keeping the documents up to date takes perhaps a tenth of each session. There's also a cost at the start: the agent has a few files to read before it can get to work, and that uses some of its context window. On my longer builds, that's more than paid for itself. I spend less time explaining where we left off, and we're less likely to redo work or reopen decisions we already made.

The agent can still be wrong. The rules help me spot mistakes and undo them.

These rules are instructions, not locks. An agent can still skip one, most often late in a long session. For the few rules where a single skip does real damage, a hook (in Claude Code, a small check that runs automatically, for example before every command) can make the rule impossible to break. Mine refuses history-rewriting git, the rule behind the first scar in `scars.md`. Another won't let a session finish while a program it started is still eating CPU: one forgotten background run held a core at full speed for five hours. Ask your agent to set one up, have it explain in plain English what it blocks, and watch it refuse a test command before you trust it.

## License

CC0 1.0: copy, change and share any of this freely, no credit needed. See `LICENSE`.
