---
layout: post
title: "GitHub: Squash and merge VS Rebase and merge""
---

“Squash and merge” and “Rebase and merge” are two different ways to combine changes from a pull request (PR) into the target branch (e.g., main) on GitHub. Both methods affect how the history of the branch is presented after merging the changes. Here’s a breakdown of the differences:

1. Squash and Merge

When you squash and merge a PR, all of the individual commits from the branch are squashed (combined) into a single commit, and that single commit is merged into the target branch.

Key Features:

 • Single commit: All the commits from the feature branch or PR are combined into one commit.
 • Clean history: The commit history is linear and clean, showing only the final, squashed commit with the changes.
 • Commit message: You can customize the commit message that appears in the final commit, typically reflecting the entire PR rather than each individual commit.

When to use it:

 • Clean history is important: If you prefer a simple and clean history, with one commit per feature or PR, this is a great option.
 • Small, cohesive changes: When individual commits don’t need to be preserved, like when commits are more of “work-in-progress” steps.

Example:

 • If a PR has 5 commits: A -> B -> C -> D -> E
 • After squash and merge, the target branch will only get 1 commit that contains the combined changes of all 5 commits.

2. Rebase and Merge

When you rebase and merge, GitHub takes all the commits from the feature branch, rebases them (i.e., applies them) onto the tip of the target branch, and then merges them.

Key Features:

 • Preserve individual commits: All the commits from the branch are maintained in the target branch, but they are applied on top of the latest state of the target branch.
 • Linear history: The history is linear (no merge commits) but still contains each individual commit.
 • No merge commit: Unlike a traditional merge, this doesn’t create a “merge commit.” The branch’s commits are simply added to the history of the target branch in sequence.

When to use it:

 • Preserving individual commits: If the individual commits have meaningful context and should be kept (e.g., granular commits like bug fixes, documentation changes, etc.).
 • Linear history without merge commits: You want to avoid merge commits but still keep the individual changes in history.

Example:

 • If a PR has 5 commits: A -> B -> C -> D -> E
 • After rebase and merge, the target branch will get 5 individual commits, all rebased onto the latest state of the target branch.

Summary of Differences

|Feature | Squash and Merge| Rebase and Merge
|-|-|-
|Number of commits merged| One single squashed commit| All individual commits from the PR are preserved
|History style| Linear with one commit per PR |Linear with all individual commits
|Use case| Clean, concise history |Maintain granular commit history without merge commits
|Commit message| You create a single commit message |Original commit messages are preserved
|Merge commit |No merge commit |No merge commit

Both methods aim to keep a clean, linear commit history, but the choice between “Squash” and “Rebase” depends on whether you want to retain the original commit history (Rebase) or condense it into a single meaningful commit (Squash).
