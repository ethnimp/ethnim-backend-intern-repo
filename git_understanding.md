# Git Understanding

## Merge Conflicts and Conflict Resolution

### What caused the conflict?

`main` and `merge-conflict-practice` started with the same practice note. Each branch committed a different replacement for that line. The practice branch said that both branches edited the same line, while `main` said that Git paused the merge for a manual decision. When the practice branch was merged into `main`, Git reported one conflict in `git_understanding.md` because both edits replaced the same line from their common ancestor.

### How was it resolved?

In GitHub Desktop, the file’s resolution menu offered the modified file from either branch. The exercise kept the version from `main`, which described what Git did when it encountered the conflict. GitHub Desktop then showed zero conflicted files. **Continue Merge** completed the merge into `main`.

### What did the exercise show?

Git can usually combine changes in different parts of a file. When both branches replace the same line, the person resolving the conflict decides what the final file should say. Keeping one branch’s entire file worked here because the exercise changed only one line. If a file contains other edits worth preserving, review both versions and combine the relevant changes before continuing the merge. A conflict can also happen when one branch edits a file that the other branch deletes.

## Pull Requests

### Why are PRs important in a team workflow?

A pull request (PR) proposes merging changes from one branch into another. It gives teammates a place to read the diff, ask questions, suggest improvements, and see automated check results before the changes reach the shared branch. The discussion also gives the team a record of why a change was made and what reviewers considered.

### What makes a well-structured PR?

A good PR has a specific title, a description that explains what changed and why, and a diff focused on one purpose. The description should tell reviewers how the change was verified and mention the related issue when there is one. For a bug fix, a short example of the original behavior and the expected result makes it easier to review the fix and check the test coverage.

### What did I learn from reviewing an open-source PR?

Prettier PR `prettier/prettier#20557` fixed missing semicolons after class properties marked with `prettier-ignore`. In an inline comment, the reviewer flagged missing test cases and asked the author to reuse a shared list of class property types. The author pushed commits that reused the list and added tests. The reviewer later approved the PR, and it was merged.

I learned that specific feedback gives the author a clear next step and makes the revision easier to review. The added tests also gave the team a way to check that the fix covered cases the first version missed. In my own PRs, I’d explain which cases I tested and reply to review comments with what changed.
