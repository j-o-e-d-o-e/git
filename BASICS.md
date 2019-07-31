# Basics


### .gitignore

- [Templates](https://github.com/github/gitignore)
- rules in .gitignore are only applied to untracked files

- `git rm --cached <file>` removes tracked `<file>` to not be further tracked
 - useful if file has been added to .gitignore and these changes in .gitignore shall come into effect
 - as 2nd step, this change needs to be committed to repo (like remove tracked files)


### Revert a commit

- `git revert <hash>` reverts commit with specified hash by making a new commit
- e.g. `git revert HEAD` reverts commit to which HEAD currently points

- similar to retrieving older version, but for whole commit
- unlike resetting a branch, it does not move the HEAD pointer 
- useful to undo changes of an entire commit
- conflicts can arise if later commits after specified commit include changes on same line of same file


### Retrieve older version from repo

- `git checkout <hash> -- <file>` puts file from commit with specified `<hash>` in staging and working tree
- useful for making a new commit based on an older version of a file:
    - retrieve older version, e.g. from HEAD^ or HEAD^^
    - modify file in working tree
    - add file to staging tree which represents the accumulated changes
    - finally, make new commit 


### Amend last commit

- `git commit --amend -m "Comment"` adds currently staged files to last commit and sets new comment
- `amend` reverts last commit to staging tree and creates new commit out of this last commit and files in staging tree
- due to the chaining of commits, git only allows to change the last commit
- useful for changing comment for last commit or adding additional files to last commit


### Undo changes in staging tree

- `git reset HEAD <file>` moves file from staging tree back to working tree


### Undo changes in working tree

- `git checkout -- <file>` reverts tracked file
- `--` indicates current branch
- `git checkout -- .` discards all changes in working tree


### Add to stage & commit combined

- `git commit -am "Comment"` stages and commits all tracked files simultaneously (-a/--all)
- does not include untracked changes
- changed files need to be already added to staging tree via `git add`


### Commit

- `git commit -m "comment"` adds staged files to where HEAD points in the repo with a 'comment'
- `commit` moves HEAD from parent of the new commit to new commit in current branch


### Add to stage

- `git add <file>` adds `<file>`, whether tracked or untracked, to staging tree
- `git add .` adds everything in current dir
- staging tree for bundling changes into one commit, a snapshot of changes


### Remove untracked files

- `git clean -f` removes all untracked files from working tree and local drive (force)
- dry run with option `-n`, interactive mode with `-i`


### Remove tracked files

- `git rm <file>` removes tracked file from project and adds change to staging tree
- as 2nd step, this change needs to be committed to repo
- specified file is removed from working tree and local disk
- it can only be retrieved by reverting the commit since it still exists in repo


### Rename

- `git mv <file_old> <file_new>` renames file and adds change to staging tree


### Logs

- `git log -3` or `git log -n 3` shows only last three logs
- `git log --grep="<search>"` shows logs corresponding to regex `<search>`
- `git log <file>` shows changes related to specified file
- `git log --graph --all` shows graph with all branches
- `git log <branch>` shows logs for another than current branch
- `--oneline` for shortened view


### Diff

- `git diff` compares working tree to repo
- `git diff --staged` compares staging tree to repo. `--cached` can be used synonymously in this context
- `git diff HEAD^` shows difference between current and last commit, equivalent to `git diff HEAD HEAD^`
- `git diff <branch1>..<branch2>` compares two branches


### Useful

- Write commit commit messages in present tense, not past tense


## Materials

- [Tutorial](https://www.lynda.com/Git-tutorials/Git-Essential-Training-Basics-REVISION-2019-Q1/5030978-2.html)
