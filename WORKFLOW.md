1. What did the rejected push error message tell you, and why did it happen?
- Git said the push was rejected because the remote "contains work that you do
not have locally," and suggested fetching before pushing again. This happened
because the remotes feature/loyalty-points had moved forward since my last
fetch someone else pushed a commit my local branch didn't know about. Git
refuses a non fast forward push by default so a push can never silently
overwrite commits it hasn't seen. The local branch tip has to be a descendant
of the remote branch tip.

2. What's the actual difference between how you resolved Task 3 (merge) vs Task 4 (rebase)?
- The merge in Task 3 kept both histories and added a new merge commit with two
parents nothing was rewritten, and the branch structure records that two
lines of work were combined at that point. The rebase in Task 4 rewrote my
local commit on top of the new remote tip it replayed my change as if it had
been made after the other persons, producing a linear history with no merge
commit. Same conflict resolution work either way, but merge preserves the
true concurrent development shape of history while rebase rewrites commits
to fake a straight line.

3. What one habit would have avoided both rejected pushes in this lab?
- Running git fetch or git pull right before starting new work and right
before pushing. Both rejections happened because a local branch was stale
relative to the remote when a push was attempted a quick fetch first would
have surfaced the divergence immediately instead of at push time.


4. Which approach - merge or rebase - would you default to on a shared team branch, and why?
- Merge, for a branch other people are actively pushing to. Rebasing rewrites
commit hashes, so if anyone else has already pulled the branch, a rebased
push forces them into their own conflict resolution mess (or requires a
force push). Merge is safe by default because it never rewrites commits that already exist
upstream. Rebase is better reserved for cleaning up your own local, not yet shared commits before you first push them.

