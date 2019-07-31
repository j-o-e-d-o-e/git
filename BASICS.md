# Basics


### .gitignore

- [Templates](https://github.com/github/gitignore)
- `git rm --cached <file>` removes tracked `<file>` from staging area (after adding to .gitignore)


### Remove untracked files

- `git clean -f` removes all untracked files from working dir
- dry run with option `-n`


### Revert a commit

- `git revert <hash>` reverts commit with specified hash by making a new commit
- `git revert HEAD` reverts commit to which HEAD currently points


### Retrieve older version of a file

- Git only allows to amend (change) most recent commit
- `git checkout <hash> -- <file>` puts file from commit with specified `<hash>` in staging area/working dir


### Amend last commit

- `git commit --amend -m "Comment"` adds currently staged files to last commit and sets new comment
- therefore, `amend` reverts last commit to staging area and creates new commit


### Undo changes from staging area

- `git reset HEAD <file>` moves file from staging area to working dir


### Undo changes from working dir

- `git checkout -- <file>` reverts file
- `--` indicates current branch
- `git checkout -- .` removes all changes from working dir


### Add to stage & commit combined

- `git commit -am "Comment"` stages and commits all tracked files simultaneously (-a/--all)
- does not include untracked changes
- changed files need to be already added to staging area via `git add`


### Remove

- `git rm <file>` removes file in working dir and adds change to staging area
- as 2nd step this change needs to be committed to repo


### Rename

- `git mv <file_old> <file_new>` renames file and adds change to staging area


### Logs

- `git log -3` or `git log -n 3` shows only last three logs
- `git log --grep="<search>"` shows logs corresponding to regex `<search>`
- `git log <file>` shows changes related to specified file
- `git log --graph --all` shows graph with all branches
- `git log <branch>` shows logs for another than current branch
- `--oneline` for shortened view


### Diff

- `git diff` compares working dir to staging area, by default
- `--staged` and `--cached` can be used synonymously in this context
- `git diff HEAD^` shows difference between current and last commit, equivalent to `git diff HEAD HEAD^`
- `git diff <branch1>..<branch2>` compares two branches


### Useful

- Write commit commit messages in present tense, not past tense


## Materials

- [Tutorial](https://www.lynda.com/Git-tutorials/Git-Essential-Training-Basics-REVISION-2019-Q1/5030978-2.html)
