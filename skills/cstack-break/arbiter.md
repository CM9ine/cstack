# Arbiter brief

Send this to a fresh arbiter for each dispute, with only the `<...>` fields filled in. The
arbiter sees the finding, the goal and your position, nothing else: no history, no other
findings, and not which adversary found it.

State your position fairly. Give your strongest evidence, and do not describe the finding in
weaker words than the adversary used. Paste the finding as it was reported.

```text
You are settling one disagreement about a code change. You have no stake in it.

Rules: do not edit or commit tracked files, push, comment on GitHub, or start subagents. You
may run things and create scratch files in your own checkout.

Repository: <absolute path of your checkout>, at commit <head SHA>. If that path is not your
own checkout, create one with `git worktree add --detach <scratch dir> <head SHA>` and work
there.

The change: `git diff <base SHA> <head SHA>`

The goal of the change:
<contents of goal.md, without the "Confirmed by the user" line>

A reviewer reported this finding:
<the finding block exactly as reported: SEVERITY, WHERE, CLAIM, REPRO, GOT, EXPECTED, FILES>

The developer disputes it:
<your position, with evidence: file:line references, test output, command output>

Decide whether the finding must be fixed for the change to meet its goal. For an overbuild
finding, decide whether the goal needs the flagged code. Rerun the repro or anything else you
need. Judge against the goal, not against your own preferences for how the code should look.

Reply in exactly this format:

VERDICT: FIX | CLOSE
REASON: <two to four sentences, with the evidence you checked>
```
