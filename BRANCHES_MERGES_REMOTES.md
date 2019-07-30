# Branches, Merges, and Remotes


## Remotes

- branch `origin/master` is stored locally, mirrors master-branch on local machine and references remote-master-branch
- `origin/master` is the tracking branch for the remote-branch and tries to stay always in sync with remote
- generally, commit locally, fetch remote to `origin/master`, merge local commits with `origin/master` and push results to remote
- remote-branches cannot be checked out, instead new branch which tracks remote-branch has to be created
- multiple remote-branches can be added to and checked out from remote

### Pull from remote

- `git pull` does both steps fetching and merging, at once
- if no commits have been made, `pull` recommended
- otherwise, `fetch` for more fine-grained control about merge conflicts

### Fetch from remote

- `git fetch <remote>` synchronizes `origin/master` with remote
- if only one remote and due to tracking, `<remote>` can be omitted


- generally, fetch often and fetch before each push
- `fetch` saves changes from remote only to local tracking-branch `origin/master`, but changes are not merged into `master`
- therefore, `git merge origin/master` to merge `master` with `origin/master`

### Clone repo

- `git clone <url> <dir>` clones remote to `<dir>`
- if `<dir>` does not exist, directory is created
- if `<dir>` not provided, repo is stored in subdirectory with name equivalent to remote-branch


- `clone` provides access to all pushed remote-branches and adds tracking automatically

### Push to remote

- `git push -u origin master` pushes `master`-branch to `origin`-remote (alias) and  moves the `origin/master`-pointer to be in sync with `master`
- consequently, `master`, corresponding branch in `origin` and `origin/master` are in sync, again


- `-u` ensures that local `master` tracks remote and stands for 'upstream'
-  allows not to explicitly mention remote-branch for fetching, pulling and pushing
- for following pushes, `-u`-option can be omitted since tracking is already initiated
- consequently `origin master` can also be omitted ->  `git push`


- `pull` before `push` to make sure local `master` is in-sync with remote and integration succeeds

### Create local tracking branch

- `git checkout -b <branch> origin/<remote>` creates new `<branch>` which tracks remote-branch `<remote>` from `origin` and checks it out
- so, `<branch>` branches off of `origin/<remote>`

### Delete remote branch

- `git push origin --delete <branch>` deletes remote-`<branch>` from remote `origin`
- tracking branch on local machine can then also be deleted

### Add remote branch

- `git push -u origin <branch>` pushes local `<branch>` to remote and also enables tracking

### Add remote to local repo

- `git remote add origin <url>` and `git push -u origin master`
- `origin` is standard name of remote-alias
- `git remote -v` shows remotes
- remote-metadata is stored in `.git/config`
- `git remote rm origin` would delete remote-branch `origin`


## Merges

### Stash changes

- separate area apart from working dir, staging area and repo
- useful for saving changes in working dir before checking out another branch -> changes which would be overwritten


- `git stash save "name"` moves changes into stash out of the working dir -> allows checking out another branch
- `git stash list` shows list of elements in stash
- `git stash show stash@{<index>}` shows element at `<index>`
- `git stash show -p stash@{<index>}` shows patch version with changes
- `git stash pop` retrieves newest change into working dir and deletes this element from stash
- `git stash pop stash@{<index>}` retrieves specific change
- `git stash apply` retrieves newest change into working dir, but does not delete element from stash
- `git stash clear` deletes all elements from stash
- `git stash drop stash@{<index>}` deletes one element

### Resolve merge conflict

- if changes on different branches to the same line in the same file, a merge conflict arises
- if two different lines are changed, no conflict


- `git merge --abort` aborts the merge and sets back the file (not indicating the merge conflict, anymore)
- resolve manually and delete the conflict indicators in the file

### Merge branch

- `git merge <branch>` merges `<branch>` into current branch


- Fast-Forward merge:
    - no further commits on master from commit where `<branch>` branched off, but on `<branch>`
    - commits from `<branch>` will be simply added to master-timeline
    - should be no conflicts
- Non-Fast-Forward merge:
    - master has commit(s) that `<branch>` has not and vice versa
    - commits from `<branch>` are merged into current branch
    - conflicts between commits from branches can arise


- only merge with a clean working dir
- `git branch --merged` shows branches which are merged with current branch
- to undo merge, `git reset --hard HEAD^` (if one commit was merged) or `HEAD^^` (two commits)

## Branches

### Reset branch

- `reset` changes the files in the staging area and/or working dir to the state they had when a specified commit was made 
- moves HEAD to the specified commit and previous commits will be discarded
- "Make my project look like it did back then"
- Careful if commits are already shared with remote
- Mostly used within private repo and when changes are not pushed to remote, yet


- 3 reset-types:
    - SOFT:
        - `git reset --soft <commit>`
        - e.g. with `<commit> =  HEAD^` latest commit is discarded and HEAD points to last but one
        - discarded commits are moved into staging area
        - useful for making one commit out of two:
            - go back two commits with `<commit> = HEAD^^`
            - discarded commits are in staging area and can be re-committed in one commit
    - MIXED:
        - `git reset --mixed <commit>`
        - discarded commits are moved into working dir
        - default, if no option is provided
        - useful for splitting one commit into multiple commits:
            - go back one commit
            - discarded commits are in working dir and can be re-added to staging area
    - HARD:
        - `git reset --hard <commit>`
        - discarded commits are gone
        - useful to permanently undo commits:
            - undo merge
            - go back one commit
            - do sth different ...


- undo a reset
    - copy the hash from the latest commit
    - after initial reset, reset branch again with `<commit>` corresponding to copied hash to go back to that point in timeline
    - only possible if no commits have been executed in between


### Delete branch

- `git branch -d <branch>` deletes branch
- currently checked out branch cannot be deleted

### Checkout branch

- `git checkout <branch>` points HEAD to specified branch, if available
- `git checkout -b <branch>` creates new branch and checks it out
- `checkout` switches to branch, gets files from branch and puts them in working dir, if there are no conflicts
- `__git_ps1` starts script showing current branch in console

### Show/create branches

- `git branch` shows current branches
- currently checked out branch is marked with an asterisk
- `git branch -a` shows all branches including remotes, with option `-r` only remotes
- `git branch <name>` creates new branch with the specified name
- `git branch <name> <branch>` creates new branch which branches from `<branch>`


- it matters to which branch HEAD currently points when creating new branch, because the new branch branches from this branch


## Materials

- [Lynda tutorial](https://www.lynda.com/Git-tutorials/Git-Branches-Merges-Remotes/5030980-2.html)
