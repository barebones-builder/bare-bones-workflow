# Log: [YYYY-MM]

*This month's sessions, one entry each, newest at the bottom. Rename this file to the month (e.g. `2026-11.md`) and start a new one each month. Ten lines at most an entry: the log is for detail, PROGRESS for the present. Written once, at the wrap. Delete the invented example once your first entry is in.*

## Template

```
### S[n] — [what it advances] ([date])
[One or two sentences: the scope, and what asked for it.]
**What changed.** [files and functions touched; numbers, not adjectives; commit hashes for steps]
**Checks.** [tests run, by name, and their result; "not run, no change to X" for the rest]
**Sizes.** [CLAUDE.md, PROGRESS.md, this entry, the longest function touched, against their limits]
**The review.** [the before/after pair's name and what the owner said, or "waiting"; the cost if notable]
**Decisions.** [one line each, with its ID; whose; a reversal names the old row]
**Deferred.** [what was left, and where it now sits (PROGRESS, limitations)]
```

## An invented example

```
### S14 — The narrator's pauses and paragraph cuts ([date])
The owner asked for stories to "breathe"; readings also reset mid-sentence.
**What changed.** `reader.py` cuts at paragraph breaks (`split_paragraphs`, new, 22 lines); pause 0.3 → 0.6 s for stories only. Steps `a1b2c3d`, `e4f5a6b`.
**Checks.** `test_reader.py` 14 OK (3 new). Not run: the full suite (no change outside the reader).
**Sizes.** CLAUDE.md 4.6 KB; PROGRESS.md 22 KB; this entry 9 lines; longest function touched `read_story` 48 lines.
**The review.** `review/S14 pause 0.3 vs 0.6/`: owner, "the longer one lets it breathe". Cuts: waiting. $0.04 of voice.
**Decisions.** D1 the 0.6 s pause (owner); D2 paragraph cuts, reverses S6 · D3, `CUT_MODE=length` the old way (agent).
**Deferred.** Very long paragraphs still cut by length (limitations); chat pauses unchanged.
```
