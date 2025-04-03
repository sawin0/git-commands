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

### 3. To list all your commit message of certain date range.

```
git log --author="$(git config sawin0)" --since="2025-04-01" --until="2025-04-01 23:59:59" --oneline
```
 - Note: You can adjust the --since and --until dates to any range you prefer.

</br>

### 4. To stages all tracked (but not new) changes and commits them with the provided message in one step.

```
git commit -am "Commit Message"
```

</br>

### 5. To rebase the entire commit history, starting from the root commit, and amends each commit to reset the author to the current user without changing the commit message. Note: This command will edit the commit date too.

```
git rebase -r --root --exec "git commit --amend --no-edit --reset-author"
```

</br>

### 6. To rebase the entire commit history while preserving the date.
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

### 7. To remove all the files that must be git ignored:
  - Update your .gitignore file and run the following command

```
git rm -r --cached .
```

 - And finally commit and push the changes.

</br>

### 8. To cherry pick multiple commits:

```
git cherry-pick 959f6bf4097bb565c2bef105964d5fb2437bd644^..d89446838c73a66585d12a04a16dc6c16b728f3a
```

</br>

### 9. To amend the most recent commit by setting both the commit author and committer date to yesterday's date without changing the commit message.

```
GIT_COMMITTER_DATE="$(date -v -1d "+%Y-%m-%dT%H:%M:%S")" git commit --amend --no-edit --date "$(date -v -1d "+%Y-%m-%dT%H:%M:%S")"
```

 - Note: You can replace -1d with any other number of days to adjust the date accordingly (e.g., -5d for 5 days ago, -10d for 10 days ago, etc.).
