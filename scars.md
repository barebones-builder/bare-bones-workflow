# Scars: what went wrong behind each rule

*Every rule in the template is here, with what went wrong to create it, ordered by how much damage the incident did, worst first. Sources: seven projects' rule files, decision rows, logs, retros and the agents' own notes. Where nobody wrote down why a rule exists, it says "origin not recorded"; nothing here is guessed.*

## How the method grew

It started in **a first project**: about six months of a hobby app built entirely by an AI agent. That's where most of the hard rules came from, each with a dated lesson attached: never rewrite a whole file, commit as you go, no history-rewriting git, the documents must agree at every session boundary, and an automated check passing doesn't prove the thing is right. It also ran a monthly retro that named the month's hardest moment.
Then, over about six weeks, the rules passed through **five more projects**, each starting from the last one's rules and cutting them down for weight. Along the way came the decision round (decisions scattered through an evening kept stopping the build), every file explaining itself (explaining code back in chat cost more than it taught), sizes measured every session (the limits were routinely broken), three decisions at most, and documents written once at the wrap (per-step rounds had become too many commits to follow).
**The latest project**, the seventh, took the previous one's rules, cut down again on day one. Over a month of daily sessions it added the crash check, one writer at a time, asking before every paid run, "is it worth it?", the wider owner/agent split of decisions and outside reviewers. A review of the whole setup at the end of that month added one reviewer per question, a fresh read of every brief, and a new place retiring an old one.
Two lessons run through all seven. **A rule is earned by a failure, not by sounding sensible** (the first project rolled back a session-end gate the same day it was added, because the habit it enforced had never actually failed). And **a rule trimmed without a check that enforces it comes back as damage**: the first project dropped a file-integrity rule and files were corrupted.

## Lost work

**1. No history-rewriting git; commit each step that runs green** *(rule 12)*
First project: a session reached for a rebase, hit a snag, aborted it under pressure, and silently wiped a day of uncommitted drawing work. Commits are cheap; redrawing isn't.
It has been carried, unchanged, into every project since. It is now also locked: a hook refuses rebase, `reset --hard` and force-pushes before they run, so the rule no longer depends on the agent remembering it.

**2. Approved work lives in the repo, not in the tool that made it** *(CLAUDE.md, Outside eyes; also the README's design-model row)*
The latest project: the design model kept its approved studies in its own app's session folders, and when the owner deleted old sessions for privacy, a week of studies went with them. Not in git, not in the bin; five checks failed with "study not found".
They were rebuilt from the assets that survived. The agent now copies every approved handoff into the repo the day it wires it.

**3. Surgical edits, the diff read before the commit** *(rule 8)*
First project: rewriting a long file risked the agent's output limit silently chopping off its end. Later, a file-integrity rule was trimmed with no check to back it, and files were corrupted.
Sharpened in the previous project (config files edited as text at one spot, never regenerated). Here, reading the diff caught a stream editor changing every line ending and a heredoc that ate backslashes so a patch matched nothing.

**4. Nothing is undone silently** *(rule 4)*
Earlier projects' decision logs already said "a decision that is undone gets a new row that names the old one" (origin there not recorded). The latest project's day one is the scar: two things built that morning were reversed by afternoon, and nobody knew whether anyone had heard the before and after, "because nothing was written down".
The switch that keeps the old way reachable until the owner has tried both was added here.

**5. Crash check** *(the session's shape)*
First project: the charter still listed the checker as work to do weeks after the checker had shipped, so sessions had to stop and ask whenever the pointer and the charter disagreed. Another project opened a session to find two finished stages uncommitted and the plan still a stage behind. The latest project: a session hit its usage limit before the wrap and left nine files uncommitted with no notes, and the next session was told "see PROGRESS", which knew nothing.
Writing the documents once at the end is tidy, until the end never comes.

## Silent errors and near misses

**6. The owner's eye and ear are the gate** *(About the owner)*
First project: a shape change passed every automated check and still looked wrong on screen, which led to the lesson that a passing check is needed but says nothing about how it looks. The previous project: the owner couldn't judge feel from sliders or from three written options ("I can't figure out which way to take it"), so choices went behind switches to be tried by hand. Two other projects: the checks were green while the real screen showed the fault, and only the owner looking caught it ("seeing it caught what the tests had not").
Here it is the ear: a before/after pair in a folder.

**7. Never loosen a test to pass** *(rule 9)*
The previous project: the test runner ran nothing, exited cleanly, and the script reported green. "A green that proves nothing is worse than red." Another project: a filtered test run matched nothing and reported "not run", "which reads exactly like a pass". The latest project: timing checks failed a different way on each of three runs, a retry was the obvious fix, and the cause turned out to be the checks' own screenshot.
A retry would have hidden the bug in the check.

**8. Test what the change could affect** *(rule 9)*
Earlier projects ran every test before the last commit. Here the full gate, in the owner's words, "literally bring[s] my laptop to a standstill".
So each session runs its own suites by name and logs what it didn't run. The price, twice here: a check went stale unnoticed between full runs and failed when it finally ran. So the rule now reads "what the change could affect", not just what the session touched.

**9. Sizes measured; at the limit, move and never delete** *(rule 11)*
First project: the next-session pointer, meant to be a few lines, grew past 700 lines of closed sessions; a trim check followed. Another project: the rules file doubled in four days (10.6 KB to 19 KB), and every session start cost about 17,000 tokens before any work. Another: the limits were routinely broken (the next-session file twice its limit) until sizes were measured every session. The previous project: PROGRESS was trimmed six times in a session, then got a rolling window. The latest project: the cap was raised eight times, from 8 KB to 45 KB.
At 44,993 of 45,000 bytes, a whole section moved word for word to its own file, leaving a pointer. Nothing was trimmed.

**10. One variable at a time** *(rule 2)*
The previous project: "one thing at a time, so the drive can say which". The latest project: a sound-effect comparison came back "both still sound a little bolted on", but the takes differed in the speech and in the effect's random pitch, so nobody could tell which change helped.
The fix: one render of the words, saved with and without the effect.

**11. Deleting files needs a list checked against the backup, never a count** *(rule 14)*
The latest project: the first clear-out plan treated "heard" as disposable and counted moves within the same drive as space saved. An outside reviewer caught it before anything was lost.
Removal now goes by a file-by-file list checked by hash against the backup.

**12. One writer in the code at a time** *(rule 3)*
The latest project, from day one, with its reason written: the app was one large file, and "two sessions editing it at once undo each other". No incident was recorded before it. Then two sessions in one folder picked the same session numbers, and another session's uncommitted changes sat in most of the files this one had to commit.
Committing whole files would have swept that work into the wrong commit.

**13. Private material and secrets stay out of the repo** *(rule 6)*
First project: the repo was going public, so third-party copyrighted art was never bundled. The secrets rule came from an earlier project and returned in the previous one when a backend brought keys ("a secret in a diff stops the session"). Another project: real names got into a log entry, a decision row and a commit message. The documents were fixed by a new commit; the commit message stayed, because removing it would mean rewriting history.
The latest project: a test greeting with memory switched on was "one quit away from becoming a note about" the owner.

**14. A fresh read of every brief; a sent brief is never changed** *(`docs/outside-reviews.md`, the brief)*
The latest project, over three days: briefs to other labs' models went out with wrong counts, file paths garbled by escape characters, a real name that should have been renamed, the wrong brief, and claims about the code that weren't true. One reviewer, given no numbers, invented its own; another designed around a gap in the description.
Now a new agent that didn't write the brief reads it cold before it goes. The first check caught a garbled path about to go to two reviewers at once. A brief that has been sent is corrected in a new copy, so the record shows exactly what each reviewer saw.

## Cost and patience

**15. Ask before every paid run** *(About the owner)*
The latest project: the agent started 48 paid test replies (about 60 cents) without asking. The owner asked to be asked first. Asking before every batch then became its own chore, so it was loosened to a standing yes under a set amount per run and per week.
It lasted a day: the agents' test runs that day cost about $4, more than eight times what the app's real use cost (under 50 cents). The owner: "Set test runs to 0 - so ask me." Every paid run is now asked first, with the count and the cost, and tests use a cheaper model wherever one can stand in.

**16. Is it worth it?** *(About the owner)*
The latest project: many sessions in, the owner said, "I am not fully tracking what we're testing." When the agent put a fault in plain terms (how often it happens, what it looks or sounds like) and asked whether it was worth the effort, the owner dropped a costly line of work in one message.
Now every test, fix and result comes with that framing, unasked, and "can you live with it?" is a real option. The owner's verdict a day later: "possibly one of the most helpful things from my end of all the rules."

**17. Outside eyes check, they don't steer** *(About the owner)*
The first project ran fresh-eyes audits; one review flagged the same missing test twice, months apart. The latest project: relaying another lab's model as coordinator used up the owner's plan fast, several of a challenger's points were already built or would have misfired, and another model cited papers that don't exist.
So reviewers challenge at two checkpoints and every claim is checked against the code.

**18. One reviewer per question; never a review of a review** *(About the owner)*
The latest project, at its busiest: a review of the whole setup found the owner carrying notes by hand across about 25 AI conversations a day. One model had been asked to read another's review, then to compare two reviews. Who did what had been re-decided four times in three days and was written in six places that no longer agreed.
Now each question gets one outside reviewer, a second only before money is spent or something hard to undo, and who does what is written in one place that everything else points to.

**19. A new place retires an old one; one tray out, one tray in** *(rule 15)*
The same review found 13 places a note could be waiting, and new folders and routines added without the old ones being retired. Replies from other models landed loose on the desktop, and the owner had to tell each session where to find them. The owner: "no wonder I'm feeling the pain."
Now anything new says what it replaces, and the old one goes in the same session. Briefs go out from one folder; every reply comes back to one other, under any name, and the next session files it.

**20. No review pages; at most three things waiting** *(About the owner)*
The latest project: the agent built a waveform trimmer and then a numbered audition file, and the owner said, "I think it's better I do this bit myself." The listening queue "always stacks up"; 23 old listens were once cleared in one go.
Now it's plainly named pairs in a folder, three at a time.

**21. The owner decides taste, the agent the technical; three decisions at most** *(About the owner)*
The decision round came out of a workflow review in an early project: decisions scattered through an evening each stopped the build, so they moved into one opening message. The same week the agent settled two calls by a test score without asking, and the owner made such calls the agent's, recorded and confirmed at the next round. Three at most was copied in from another project a few weeks later, as "lighter than every step up front; the cost is that some decisions wait a session" (why three: not recorded). Here the owner still made every design decision, until the load showed after an outside reviewer named it.
The agent now makes and records the technical calls.

**22. Short in chat** *(About the owner)*
First project: a silent debugging spiral left the owner watching minutes of activity with no word on what it was doing, which led to a one-line note at every milestone. The previous project: diagrams in chat cost "too much in tokens", so "a table beats a paragraph".
Carried here unchanged.

**23. One documents round, at the wrap** *(rule 12)*
First project: the documents were reconciled at every session end, so the next session would find them in agreement. Later, with sessions run back to back, the owner found the per-step rounds too many commits to follow, and the round moved to once at the end. The row that made the change wrote down its own cost: a session that breaks midway leaves more work unlogged. The previous project cut further, with one-line step commits, because it "seems to be burning more tokens than most".
Scar 5 is that cost arriving.

## Thin records

*Rules whose records are thinner than the scars above: no failure behind them, only a cost, or incidents found only in a later search. The owner's account: rules without a recorded incident came out of dedicated "review my workflow" sessions.*

- **Quality wins** (rule 7): first project, a first pass is never shipped quietly; its limitation is written down. Later projects opened with the owner's own instruction to build to the highest standard, and the previous project kept it whole when everything else was cut. No incident behind it.
- **Ideas go in PROGRESS with why not now** (rule 13): first project, side-quests go into a queue, not the session. Its workflow audit found the queue full of parked items with nothing saying when they'd be picked up, and never ruled on. Another project: an idea "booked for after" a phase was never put to the owner, and came out only when the owner asked what had been missed.
- **Every file explains itself** (rule 10): an early project found that explaining code back in chat cost a lot of tokens for what it taught, because every turn re-sends the whole session; the explanation moved into a short plain-English note at the top of each file. The previous project cut it to about fifteen lines, with history moved to the log, for token weight.
- **Behaviour lives in the prompt files, code handles delivery** (rule 5): the previous project put every feel number in one tuning file ("a game's rules are its tuned numbers"). This form: origin not recorded.
- **The medium rule** (rule 1): each project had one (one project's: "the core loop is the game"). Origin not recorded.
