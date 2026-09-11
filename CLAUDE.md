# watersmart — agent guide

## Standing authorization (owner instruction, 2026-09-11)

Follow the [Platform authorization standard](https://github.com/imnogoodatthis-dev/platform/blob/main/docs/standards/agent-authorization.md).
Dylan's request authorizes routine diagnostics, scoped edits, task dependency
installation, tests, isolated previews, worktree setup, task-owned commits,
pushes to the existing configured origin, and PR creation/updates. Proceed
without repeated permission questions. Agents may coordinate relevant repository,
branch, ownership, PR/check status, and shared-resource scheduling with Dylan's
other verified tasks; do not share secrets, personal records, or message others.

Agents may merge this repository's PRs into `main` when all required checks and
agentic review pass for the current PR head, with no unresolved HIGH/MEDIUM
findings or owner hold. Verify reviewer requirements and mergeability, recheck
the head immediately before merging, and use an expected-head guard. Missing,
stale, running, failed, or unexpectedly skipped required checks are not green;
never bypass a gate, directly push `main`, or invent a passing review. Establish
an explicit validation/review path if required checks are absent. Normal
deployment through the documented merge/release workflow is authorized. The
Asheville-Tutoring exception in the shared standard does not apply to this repo.

Keep resource ownership, integration validation, credentials, destructive live
operations, and physical-device safeguards in force. Use authorization already
given for an exact action; do not ask for it again. If blocked, name the action
and specific rule or auto-review denial after completing independent preparation.

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
publishing destination. Never push directly to `main`; merge the reviewed PR
only after the standing authorization gates above pass. Read README.md for integration setup. Validate
changes in isolated test state; coordinate and obtain the existing required
permission before changing the live Home Assistant installation or actuating
physical devices. Updating documentation does not deploy the integration.

The fork currently has lint, pytest, HACS, and Hassfest workflows but no
agentic-review workflow. Verify which checks actually run and are required;
record independent review against the current PR head before considering a
merge. An absent review workflow is not evidence of approval, and required
checks disabled in a fork are not automatically waived.
