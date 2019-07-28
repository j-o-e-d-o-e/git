# Basics


## Ignore

### .gitignore

- [Templates](https://github.com/github/gitignore)
- `git rm --cached <file>` removes file from staging area, if you have added it to .gitignore before and don't want it to be tracked, anymore

### Remove untracked files

- `git clean -f` removes untracked files from working dir
- dry run with option `-n`


## Undo and revert

### Revert a commit

- `git revert <hash>` reverts commit with specified hash by making a new commit
- `git revert HEAD` reverts commit to which HEAD currently points

### Retrieve older version of a file

- Git only allows to amend (change) most recent commit
- `git checkout <hash> -- <file>` puts file from commit with specified hash in staging area and working dir

### Amend last commit

- `git commit --amend -m "Comment"` adds currently staged files and sets new comment
- `amend` reverts last commit to staging area and creates new commit

### Undo changes from staging area

- `git reset HEAD <file>` moves file from staging area to working dir

### Undo changes from working dir

- `git checkout -- <file>` reverts file. `--` indicates current branch
- `git checkout -- .` removes all changes from working dir


## Add, remove, rename

### Add to stage & commit combined

- `git commit -am "Comment"` stages and commits all tracked files simultaneously (-a/--all)
- does not include untracked changes
- changed files need to be already added to staging area via `git add`

### Remove

- `git rm <file>` removes file in working dir and adds change to staging area
- as 2nd step this change needs to be commited to repo

### Rename

- `git mv <file_old> <file_new>` renames <file> and adds change to staging area.


## Infos

### Logs

- `git log -3` or `git log -n 3` shows only last three logs
- `git log --grep="<search>"` shows logs corresponding to regex
- `git log <file>` shows logs about changes related to the specified file
- `git log --graph --all` shows graph with all branches
- `git log <branch>` shows logs for another than current branch
- option `--oneline` for shortened view

### Diff

- `git diff` compares working dir to staging area, by default
- `--staged` and `--cached` can be used synonymously in this context
- `git diff HEAD^` shows difference between last and current commit -> equalivalent to `git diff HEAD^ HEAD`
- `git diff <branch1>..<branch2>` compares two branches


## Useful

- Write commit commit messages in present tense, not past tense


## Materials

- [Lynda tutorial](https://www.lynda.com/Git-tutorials/Git-Essential-Training-Basics-REVISION-2019-Q1/5030978-2.html)
