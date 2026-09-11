# watersmart — agent guide

## Task worktrees and cleanup

Keep the canonical checkout on `main` as the stable integration/runtime
checkout. Each independent writing task uses its own Git worktree and unique
feature branch from freshly fetched `origin/main`; edit, install dependencies,
test, and preview there. Never switch the stable checkout to a task branch.
Use managed worktrees or `C:/Users/dylan/Code/.worktrees/<repo>/<task>` locally;
use a designated development directory on other hosts. An already isolated cloud
task checkout needs no additional worktree. Separate task worktrees may work
concurrently, even on the same source files.

Read the [shared worktree lifecycle](https://github.com/imnogoodatthis-dev/platform/blob/main/docs/standards/local-checkouts.md).
Keep task ownership explicit; stage only named files belonging to this task.
Never alter another task's files, stashes, branch, or unsaved editor state.
Worktrees do not isolate ports, credentials, databases, containers, or shared
editors: use task-local preview resources and coordinate live changes to the
same resource. Existing merge permissions and deployment guardrails still apply.

Ship via a reviewed PR to `main`. After a confirmed merge into `dev` or
`main`, audit the PR's merged head (including squash/rebase), later commits,
dirty/untracked/ignored files, and active sessions. Preserve any remaining work,
stop only task-owned previews, remove that specific registered worktree from
outside it, and delete only the safely completed feature branch. Never force
worktree removal, run blanket cleanup, or delete long-lived integration branches.
Coordinate a clean stable checkout's `git pull --ff-only` after merge; never
reset another session's work. If handing off an open PR, record its worktree path,
branch, owner, and pending cleanup for the agent handling the merge or next session.
These instructions do not install unattended cleanup.

## Repository and live installation

For Dylan's fork, use its existing configured `origin` (`ImNoGoodAtThis/watersmart`)
for task branches and PRs. `upstream` (`wbyoung/watersmart`) is not the default
publishing destination. Never push or merge directly to `main`; leave the PR for
Dylan after applicable checks. Read README.md for integration setup. Validate
changes in isolated test state; coordinate and obtain the existing required
permission before changing the live Home Assistant installation or actuating
physical devices. Updating documentation does not deploy the integration.
