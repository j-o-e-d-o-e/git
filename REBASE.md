# Rebase

- take commits from one branch and replay them at the end of another branch
- useful to integrate recent commits from another branch without merging
- scenario might be:
    - commits have been made on master- and feature-branch
    - a rebase then shifts the commits of feature-branch to the tip of the master-branch
    - shifted commits are those commits on the feature-branch which came after the common ancestor-commit of master- and feature-branch
    - since the parent of each shifted commit has changed, their hashes also change
- golden rule:
    - 'Thou shalt not rebase a public branch.'
    - rebase abandons existing, shared commits and creates new, similar commits instead
    - therefore, collaborators would see the project history vanish
    - rebasing should be only used on local, private branches


### Merging vs. rebasing

- two ways to incorporate changes from one branch into another branch:


| Merge                                     | Rebase                                              |
| ------------------------------------------|:---------------------------------------------------:|
| adds merge-commit                         | no additional merge-commit                          |
| non-destructive                           | destructive: hash changes, commits are re-committed |
| complete record of what happened and when | no longer complete record                           |
| easy to do with hard-reset                | tricky to undo                                      |
| logs can become cluttered, non-linear     | logs are cleaner, more linear                       |


- merge is useful:
    - to bring a large feature-branch back into the master-branch
    - anytime the feature-branch is already public and used by others
- rebase is useful:
    - to add minor commits from master- to a feature-branch
    - to move commits from one branch to another


### Rebase commits

- `git rebase <newbase>` uses `<newbase>` as the new base for the current branch, i.e. current branch then branches off the tip of `<newbase>`
- `git rebase <newbase> <branch>` checks out `<branch>` and uses branch `<newbase>` as the new base for `<branch>`, i.e. commits on `<branch>` are shifted


### Rebase *onto* other branches


- `git rebase --onto <newbase> <upstream> <branch>` rebases `<branch>` onto `<newbase>` from `<upstream>`
- `<upstream>` is the old branch from which `<branch>` branched off before the rebase
- it defines the ancestor-commit after which the following commits on `<branch>` are to be rebased
- to undo, simply switch `<newbase>` and `<upstream>`


### Undo a rebase

- undoing complex rebases may lose data
- `git reset --hard ORIG_HEAD` undoes rebase unless `ORIG_HEAD` has changed again in the meantime
- `ORIG_HEAD` is a temporary variable git uses to keep track of where the HEAD was before a rebase, reset or merge
- alternatively, `git rebase --onto <commit> <upstream> <branch>` rebases to former merger-base specified by `<commit>`


### Handle conflicts

- git pauses the rebase before each conflicting commit
- similar to resolving merge-conflicts:
    - manually edit files and delete conflict-indicators
    - `git add <file>` to add specified `<file>` to staging tree
    - but, instead of `git commit` (when merging) use then `git rebase --continue`
    - continue with the conflict in the next file of the rebase...
- `git rebase --skip` skips the to-be-rebased commit, e.g. if one prefers the already existing change
- `git rebase --abort` stops rebase altogether


### Pull rebase

- fetch from remote, then rebase instead of merge
- useful to keep history cleaner by avoiding merge-commits
- only use on local commits which are not yet shared to a remote
- `git pull --rebase` pulls changes from remote and rebases local changes instead of merging remote changes into local (or `-r`)
- `git pull --rebase=perserve` preserves locally created merge-commits


### Squash commits

- fold two or more commits into one commit
- e.g. `git rebase -i HEAD~3` rebases last three commits onto the same branch
- every commit since `HEAD~3` is rebased, but with the opportunity to modify them in the interactive mode
- in file `git-rebase-todo`, use `squash` instead of `pick` to meld this commit into previous commit
- `fixup` is like `squash`, but discards the commit's log message
- after editing and closing `git-rebase-todo`, rebase is performed with only one commit
- useful for cleaning up multiple commits into one


### Interactive rebasing

- chance to modify commits as they are being replayed
- `git rebase -i <newbase> <branch>` starts interactive mode and opens editor for committing changes


## Materials

- [Tutorial](https://www.lynda.com/Git-tutorials/GIT-Intermediate-Techniques/664821-2.html)