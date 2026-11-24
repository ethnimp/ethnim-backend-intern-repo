# Git Setup and What I Learned

I ran `git --version` on my Mac and confirmed that Git 2.54.0 (Apple Git-157) was already installed. I also checked that my local copy of the internship repo was on `main` and connected to GitHub.

## Have you used Git before? If so, in what context?

Yes. I’ve used Git in university projects to track changes to my code and my team's code. That’s where I got comfortable making commits and pushing them to a remote repository. I’ve also used Git to keep my Focus Bear onboarding write-ups on GitHub.

## Which Git client (if any) did you choose? Why?

I chose GitHub Desktop because I can see which branch I’m on, review the files in a change and see which commits are waiting to be pushed. It also gave me a clear way to choose which version of a file to keep during the practice merge. I read about VS Code’s Source Control view, which can show a diff beside the code I’m working on. GitHub Desktop is the interface I’m already comfortable using for this repo.

## What was the most interesting thing you learned about Git today?

The most interesting part was seeing what Git records after a merge conflict. In the practice exercise, both branches changed the same line, and I kept `main`’s version in GitHub Desktop. The merge commit still had two parents, one from each branch. I could see both branches’ commits in the history even though the final file kept just one version of the line.
