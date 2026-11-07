# Filing the PR

## Before you open it

1. Check whether a PR for this branch already exists: `gh pr view --json url,state,body`. If one
   does, update its title and description instead of opening a second one.
2. Rebase onto the latest default branch (`git fetch origin`, then `git rebase origin/<default>`).
   If the rebase needed conflict fixes, recheck as the table in [babysit.md](babysit.md) says
   before you push. A clean rebase with an identical patch needs nothing.
3. Review the full diff against the base yourself. It should contain the change and nothing
   else.
4. Push the branch.

## Title

PR titles usually become commit messages, so follow the repo's conventions. Look at recently
merged PRs and the git log. Prefer a short, readable title that says why the change matters:

> ❌ perf(server): negotiate permessage-deflate on the websocket
>
> ✅ perf(server): cut websocket frame size by 70%+ with gzipping

## Description

Open with the problem in plain words, taken from the confirmed goal in `goal.md`. Then explain
the solution briefly. Do not lead with a list of everything you changed:

> ❌ Removed implicit workspace carry-over from every "new thread" entry point (cmd+n,
> sidebar buttons, command palette). Deleted buildContextualThreadOptions and the v1 sidebar's
> seed-context machinery.
>
> ✅ My "new worktree" default was ignored when starting new threads on existing worktrees.
> Super unintuitive. Now your preferences always apply.

Then, in this order, leaving out any part with nothing to say:

1. **Data shape**, for a feature: the structure from `cstack-build` step 3, in a sentence or two.
2. **Proof**: one or two lines from `proof.md` on how you proved it works, such as the repro
   before and after, or what you saw in the app. Attach screenshots when they help and you can
   upload them.
3. **Decisions**: choices you made without asking the user, one line each.
4. **Follow-ups**: nits and out-of-scope items you declined, one line each.
5. **Break loop**: the output of `../cstack-break/scripts/report`, pasted whole, markers included.
6. **Last line**: the model and harness that made the change, for example
   `Created with Claude Opus 5.5 in T3 Code.` Use the name the harness reports, and never guess
   one. If the harness gives its own attribution lines for PRs, use those instead.

## Opening it

Before submitting, check the title, description, quotes and attachments for secrets and
private details.

Open a real PR, not a draft, so review bots run: `gh pr create --title ... --body-file ...`. If
that fails because the GraphQL rate limit is used up, use REST instead:
`gh api repos/<owner>/<repo>/pulls -f title=... -f head=... -f base=... -F body=@<file>`.

If the harness asks you to link PRs you create (T3 Code does), link it right away.

## Updating the break-loop section

After a post-PR round, regenerate the section with `../cstack-break/scripts/report` and replace
everything between `<!-- cstack-break:start -->` and `<!-- cstack-break:end -->` in the PR body.
Edit the description with `gh pr edit --body-file`. Do not post the results as a comment.
