# The goal step

Every cstack run starts here: `cstack-build`, `cstack-fix`, and `cstack-break` when it runs on
its own without a goal. The goal is what every adversary judges the change against, so a
wrong goal makes the whole loop wrong. Write it, get the user's OK, then freeze it.

## 1. Understand the request

Read the user's message and enough of the code to understand it: the files involved, how the
behavior works today. Change nothing yet.

If the message contains "full send", remember it for step 4. It decides how the run ends. It
does not skip the user's OK in step 3.

## 2. Write the goal

```markdown
**Goal:** what the user wants, in one or two sentences, in your own words.
**Problem:** what is wrong or missing today, and who notices.
**Smallest change:** the least you expect to change to meet the goal.
**Out of scope:** what this deliberately leaves alone. Write "nothing noted" if empty.
**Done when:** a check that can pass or fail, such as a command and its expected output, or
what you will see in the app.
```

Use plain words. Name real files or symbols only when they make the goal clearer. The
"Smallest change" line matters later: the adversaries flag code beyond it as overbuilt.

If the evidence already shows the request is wrong (the bug is not a bug, the feature exists),
say so with the evidence instead of writing a goal, and stop.

## 3. Wait for the user's OK

Ask with the harness's question tool, so the thread shows it is waiting: `AskUserQuestion` in
Claude Code, `request_user_input` in Codex. Put the whole goal text in the question itself,
because the user may see only the question. Offer "Looks right" and "Change it". If there is no
question tool, end your turn with the goal as your last message and ask for an OK.

Do not start work before the OK. If the user corrects the goal, rewrite it and ask again.

## 4. Freeze it

1. If you are on the default branch, create a branch first. Follow the repo's naming if it has
   one, otherwise `feat/<slug>` for a build and `fix/<slug>` for a fix.
2. Create the state folder ([record.md](record.md)) and write the confirmed goal to
   `$STATE/goal.md`, with a last line `Confirmed by the user: <ISO time>`.
3. Write `full-send` to `$STATE/ending` if the user said "full send", otherwise `full-stop`.

From now on `goal.md` is frozen. Never reword it to fit the code. Only the user can change it.
If they do, rewrite it, add the change to the `note` of the current row in `rounds.tsv`, and
tell them which earlier findings the change affects.
