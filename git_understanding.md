# Git Understanding

## Merge Conflicts and Conflict Resolution

### What caused the conflict?

`main` and `merge-conflict-practice` started with the same practice note. Each branch committed a different replacement for that line. The practice branch said that both branches edited the same line, while `main` said that Git paused the merge for a manual decision. When the practice branch was merged into `main`, Git reported one conflict in `git_understanding.md` because both edits replaced the same line from their common ancestor.

### How was it resolved?

In GitHub Desktop, the file’s resolution menu offered the modified file from either branch. The exercise kept the version from `main`, which described what Git did when it encountered the conflict. GitHub Desktop then showed zero conflicted files. **Continue Merge** completed the merge into `main`.

### What did the exercise show?

Git can usually combine changes in different parts of a file. When both branches replace the same line, the person resolving the conflict decides what the final file should say. Keeping one branch’s entire file worked here because the exercise changed only one line. If a file contains other edits worth preserving, review both versions and combine the relevant changes before continuing the merge. A conflict can also happen when one branch edits a file that the other branch deletes.
