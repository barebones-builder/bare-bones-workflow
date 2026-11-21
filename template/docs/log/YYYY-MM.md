# Log: [YYYY-MM]

*This month's sessions, one entry each, newest at the bottom. Rename this file to the month (e.g. `2026-11.md`) and start a new one each month. Ten lines at most an entry: the log is for detail, PROGRESS for the present. Before editing, write the heading and Scope line with the starting commit and mark the entry *in progress*. Record explicit owner approvals on the Decisions line as they happen. Finish that same entry at the wrap and remove the marker. A small session (CLAUDE.md rule 12) adds *small* to its title and may leave out the lines that don't apply, often Sizes and The review. Delete the invented example once your first entry is in.*

## Template

```
### S[n] — [what it advances] ([date])
**Scope.** [what was agreed and the starting commit]
**What changed.** [files and functions touched; numbers, not adjectives; commit hashes for steps]
**Checks.** [tests run, by name, their test count and result; "not run, no change to X" for the rest]
**Sizes.** [CLAUDE.md, PROGRESS.md, this entry, the longest function touched, against their limits]
**The review.** [the before/after pair's name and what the owner said, or "waiting"; the cost if notable]
**Decisions.** [ID or earlier session, whose call and why. Record any explicit owner approval here when given. Link to decision rows if used.]
**Deferred.** [what was left, and where it now sits (PROGRESS, limitations)]
**Friction.** [optional: what in the workflow itself felt heavy or confusing this session; read at the decision round]
```

## An invented example

```
### S14 — The narrator's pauses and paragraph cuts ([date])
**Scope.** The owner asked for stories to “breathe”, and readings reset mid-sentence. Started from `789abcd`.
**What changed.** `reader.py` cuts at paragraph breaks (`split_paragraphs`, new, 22 lines); pause 0.3 → 0.6 s for stories only. Steps `a1b2c3d`, `e4f5a6b`.
**Checks.** `test_reader.py` 14 OK (3 new). Not run: the full suite (no change outside the reader).
**Sizes.** CLAUDE.md 4.6 KB; PROGRESS.md 22 KB; this entry 9 lines; longest function touched `read_story` 48 lines.
**The review.** `review/S14 pause 0.3 vs 0.6/`: owner, "the longer one lets it breathe". Cuts: preview waiting for the owner. $0.04 of voice.
**Decisions.** D1 the 0.6 s pause (owner); D2 paragraph cuts, reverses S6 · D3, `CUT_MODE=paragraph` previews the new way (agent).
**Deferred.** Very long paragraphs still cut by length (limitations); chat pauses unchanged.
**Friction.** Two decision rows for one small change felt like more writing than the change.
```
