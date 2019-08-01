# Merges


### Stash changes

- separate tree apart from working tree, staging tree and repo
- useful for saving conflicting changes in working tree before checking out another branch -> otherwise, changes would be overwritten


- `git stash save "name"` moves changes from working tree into stash -> allows checking out another branch
- `git stash list` shows list of elements in stash
- `git stash show stash@{<index>}` shows element at `<index>`
- `git stash show -p stash@{<index>}` shows patch version with changes
- `git stash pop` retrieves newest change into working tree and deletes this element from stash
- `git stash pop stash@{<index>}` retrieves specific change
- `git stash apply` retrieves newest change into working tree, but does not delete element from stash
- `git stash clear` deletes all elements from stash
- `git stash drop stash@{<index>}` deletes one element


### Resolve merge conflict

- if changes on different branches to the same line in the same file, a merge conflict arises
- if two different lines are changed in the same file, no conflict
- conflicts are indicated in the following order: `<<< HEAD`, state of current branch, `===`, state of the to be merged `<branch>` and `>>> <branch>` 


- 2 basic strategies:
    - `git merge --abort` aborts the merge and sets back the file (not indicating the merge conflict, anymore)
    - resolve manually, delete the conflict indicators in the conflicted file, add and commit changes (`git commit`)


### Merge branch

- `git merge <branch>` merges `<branch>` into current branch


- Fast-Forward merge:
    - no additional commits on master from commit where `<branch>` branched off, but on `<branch>`
    - commits from `<branch>` will be simply added to master-timeline
    - should be no conflicts
- Non-Fast-Forward merge:
    - master has commit(s) that `<branch>` has not and vice versa
    - commits from `<branch>` are merged into current branch
    - conflicts between commits from branches can arise


- only merge with a clean working tree
- `git branch --merged` shows branches which are merged with current branch
- to undo merge, `git reset --hard HEAD^` (if one commit was merged) or `HEAD^^` (two commits)


## Materials

- [Tutorial](https://www.lynda.com/Git-tutorials/Git-Branches-Merges-Remotes/5030980-2.html)
