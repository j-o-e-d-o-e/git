# GIT

## Branches, Merges, and Remotes

[Lynda tutorial] (https://www.lynda.com/Git-tutorials/Git-Branches-Merges-Remotes/5030980-2.html)

### Stash changes

- separate area apart from working dir, staging area and repo
- useful for saving changes in working dir before checking out another branch -> changes which would be overwritten
- `git stash save "name"` moves changes into stash out of the working dir -> allows checking out another branch
- `git stash list` shows list of elements in stash
- `git stash show stash@{<index>}` shows element at <index>
- `git stash show -p stash@{<index>}` shows patch version with changes
- `git stash pop` retrieves newest change into working dir and deletes element from stash
- `git stash pop stash@{<index>}` retrieves specific change
- `git stash apply` retrieves newest change into working dir, but does not delete element from stash
- `git stash clear` deletes all elements from stash
- `git stash drop stash@{<index>}` deletes one element

### Resolve merge conflict

- if edits on different branches to the same line in the same file made, a merge conflict arises
- if two different lines are changed, no conflict
- `git merge --abort` aborts the merge and sets back the file (not indicating the merge conflict, anymore)
- manually and deleting the conflict indicators in the file

### Merge branch

- `git merge <branch>` merges branch into current branch
- always run merges with a clean working dir
- `git branch --merged` shows branches which are merged with current branch
- to undo merge, `git reset --hard HEAD^` or `HEAD^^`, if two commits were merged

- Fast-Forward merge
  - no further commits on master from commit where <branch> branched off, but on <branch>
  - commits from <branch> will be simply added to master timeline
  - should be no conflicts
- "Real" merge
  - commits also on master -> master has commit(s) that <branch> has not and vice versa
  - commits from <branch> are merged
  - conflicts between commits from branches can arise

### Reset branch

- `reset` changes the files in the staging area and/or working dir to the state they had when a specified commit was made -> moves HEAD to the specified commit
- Previous commits will be discarded
- "Make my project look like it did back then"
- Careful if commits are already shared with remote
- Mostly used only within private repo and changes are not pushed to remote, yet
- to undo a reset, copy the hash from the latest commit and after initial reset, reset branch again with <commit> = copied hash to go back to that point in timeline -> only possible if no commits have been executed in between

- 3 reset-types:
 - SOFT:
  - `git reset --soft <commit>`, e.g. with <commit> =  HEAD^ latest commit discarded, HEAD points to last but one
  - moves HEAD and discarded commits into staging area
  - useful for making one commit out of two -> go back two commits with <commit> = HEAD^^ -> discarded commits are in staging area and can be re-committed in one commit
 - MIXED:
  - `git reset --mixed <commit>`
  - moves HEAD and discarded commits into working dir
  - default, if no option this type is used
  - useful for splitting one commit into multiple commits -> go back one commit -> discarded commits are in working dir and can be re-added to staging area
 - HARD:
  - `git reset --hard <commit>`
  - moves HEAD amd discarded commits are gone
  - useful to permanently undo commits, e.g. undo merge -> go back one commit -> do something different ...

### Delete branch

- `git branch -d <branch>` deletes branch
- currently checked out branch cannot be deleted

### Checkout branch

- `git checkout <branch>` points HEAD to specified branch
- `git checkout -b <branch>` creates new branch and checks it out
- `checkout` switches to branch, gets files from branch and puts them in working dir, if there are no conflicts
- best to have a clean working dir before checking out another branch, not?! still, working dir is for all branches -> each branch is characterized by its commits, not the working dir
- `__git_ps1` starts script showing current branch in console

### Show/create branches

- `git branch` shows current branches. Currently checked out branched is marked with an asteriks
- `git branch <name>` creates new branch with the specified name
- it matters to which branch HEAD currently points when creating new branch, because the new branch branches from this branch

## Basics

[Lynda tutorial] (https://www.lynda.com/Git-tutorials/Git-Essential-Training-Basics-REVISION-2019-Q1/5030978-2.html)

### .gitignore

- [Templates](https://github.com/github/gitignore)
- `git rm --cached <file>` removes file from staging area, if you have added it to .gitignore before and don't want it to be tracked, anymore

### Remove untracked files

- `git clean -f` removes untracked files from working dir
- dry run with option `-n`

### Revert a commit

- `git revert <hash>` reverts commit with specified hash by making a new commit
- `git revert HEAD` reverts commit to which HEAD currently points

### Retrieve older version of a file

- Git only allows to amend (change) most recent commit
- `git checkout <hash> -- <file>` puts file from commit with specified hash in staging area and working dir

### Amend last commit

- `git commit --amend -m "Comment"` adds currently staged files and sets new comment -> `amend` reverts last commit to staging area and creates new commit

### Undo changes from staging area

- `git reset HEAD <file>` moves file from staging area to working dir

### Undo changes from working dir

- `git checkout -- <file>` reverts file. `--` indicates current branch
- `git checkout -- .` removes all changes from working dir

### Add to stage & commit combined

- `git commit -am "Comment"` stages and commits all tracked files simultaneously (-a/--all) -> does not include untracked changes
- changed files need to be already added to staging area via `git add`

### Remove

- `git rm <file>` removes file in working dir and adds change to staging area
- as 2nd step this change needs to be commited to repo

### Rename

- `git mv <file_old> <file_new>` renames <file> and adds change to staging area.

### Logs

- `git log -3` or `git log -n 3` shows only last three logs
- `git log --grep="<search>"` shows logs corresponding to regex
- `git log <file>` shows logs about changes related to the specified file
- `git log --graph --all` shows graph with all branches
- `git log <branch>` shows logs for another than current branch

### Diff

- `git diff` compares working dir to staging area, by default
- `--staged` and `--cached` can be used synonymously in this context
- `git diff HEAD^` shows difference between last and current commit -> equalivalent to `git diff HEAD^ HEAD`
- `git diff <branch1>..<branch2>` compares two branches

### Useful

- Write commit commit messages in present tense, not past tense


