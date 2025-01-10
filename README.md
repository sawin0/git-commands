# git-commands
All the Git commands with explanation that I need to do googling for my personal use

### 1. To count the number of commits that are in the local branch but not in the specified remote branch.

```
git rev-list --right-only --count origin/<remote_branch>..<local_branch>
```

</br>

### 2. To list all your commit messages for today only.

```
git log --author="$(git config sawin0)" --since=midnight --oneline
```

</br>

### 3. To stages all tracked (but not new) changes and commits them with the provided message in one step.

```
git commit -am "Commit Message"
```

</br>

### 4. To rebase the entire commit history, starting from the root commit, and amends each commit to reset the author to the current user without changing the commit message. Note: This command will edit the commit date too.

```
git rebase -r --root --exec "git commit --amend --no-edit --reset-author"
```

</br>

### 5. To rebase the entire commit history while preserving the date.
  - Create a new shell file called 'reset-author-preserve-date.sh' and paste the following code into it.

```
#!/bin/bash
export GIT_COMMITTER_DATE="$(git show -s --format=%ci HEAD)"
export GIT_AUTHOR_DATE="$(git show -s --format=%ai HEAD)"
git commit --amend --no-edit --reset-author
```
  - Then execute this command

```
git rebase -r --root --exec "./reset-author-preserve-date.sh"
```

</br>

### 6. To remove all the files that must be git ignored:
  - Update your .gitignore file and run the following command

```
git rm -r --cached .
```

 - And finally commit and push the changes.

</br>
