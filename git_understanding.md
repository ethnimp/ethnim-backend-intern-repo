# Git Understanding

## Writing Meaningful Commit Messages

### What makes a good commit message?

A good subject uses a short action phrase and names the change. If the reason matters and isn’t clear from the subject, I’d leave a blank line and explain it in the body. Each commit should have one clear purpose so that its message describes the whole change.

In the Node.js history, `fs: report EROFS from recursive mkdir()` (`a055d9f`) names the affected area, the operation and the error. The body explains that the old code could report a missing path when the real problem was a read-only file system. It also explains what the test checks. The subject `doc: fix typos in documentation` (`808904f`) gives me the general category, but I’d have to open the diff to find out which docs changed. For a small typo fix, naming the affected page would be enough.

### How does a clear commit message help in team collaboration?

A clear subject lets a teammate scan `git log --oneline` and open the commit that relates to their work. If the body explains why the behavior changed or how it was tested, reviewers have more context for checking the diff. That’s useful when someone comes back to the change later and the original author is busy or has moved on.

### How can poor commit messages cause issues later?

If several commits say `fixed stuff`, I have to open each diff to work out which one introduced a regression. That slows down debugging and makes it easier to revert the wrong change. The long subject in this exercise also took longer to scan because it included details about where I placed a paragraph. `Explain the cost of vague commit messages` is easier to pick out in the log and leaves room for a short explanation in the body.

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

## Finding a Regression with Git Bisect

### What does `git bisect` do?

`git bisect` uses binary search to find the first commit where a bug appears. I give it an older commit where the behavior works and a newer commit where it fails. Git checks out a commit between them, and each test result narrows the range. I can mark the results manually with `git bisect good` and `git bisect bad`, or let `git bisect run` repeat a test for me.

### What happened in the practice exercise?

The test repo had six commits for a small focus timer script. A 25-minute session should return 1,500 seconds. One commit changed the multiplier from 60 to 100, so the script returned 2,500 seconds. The later commits only updated the README, so the bug was still present at the tip of the branch.

In the terminal, I ran `git bisect start 247d8e0 fe48a3b` with the known bad commit first and the known good commit second. Then I used `git bisect run sh -c 'test "$(sh focus_timer.sh 25)" -eq 1500'` to check the selected versions. Git tested three commits and identified `d295b33` (`Adjust duration calculation`) as the first bad commit. Its parent returned 1,500 seconds, and its diff showed the changed multiplier. I ran `git bisect reset` to return to the original branch.

### When would I use it in real-world debugging?

If a timer worked in the previous release and started ending at the wrong time in the current release, I’d use those two releases as the starting points. I’d make a repeatable check for the timer duration and run it at the commits Git picks. Once Git finds the first failing commit, I’d inspect its diff to understand what changed and write a regression test for the fix.

### How does it compare to manually reviewing commits?

For a long history, bisect can save time because I can test a few commits and use the results to rule out whole ranges. The broken behavior also gives me a better clue than a broad commit title such as `Adjust duration calculation`. For a short history, scanning the diffs may be quicker. Bisect is most useful when the same check gives a reliable result on older versions.
