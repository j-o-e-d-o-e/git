# Branch

- for each new big feature, create a new branch
- if feature development succeeds, merge feature-branch into master-branch
- useful for isolating these features separate from dev on master
- each branch accesses the same un-staged changes, but has its own staging tree and repo


### Reset branch

- `reset` changes the files in the staging tree and/or working tree to the state they had when a specified commit was made 
- "Make my project look like it did back then"
- moves HEAD to the specified commit and later commits will be discarded
- e.g. `git reset HEAD^` moves HEAD to last but one (`HEAD^`) and discards latest commit
- Careful if commits are already shared with remote
- Mostly used within private repo
- 3 reset types:
    - SOFT:
        - `git reset --soft <commit>`
        - discarded commits are moved into staging tree
        - useful for making one commit out of two:
            - `<commit> = HEAD^^` goes back two commits 
            - all discarded commits are in staging tree and can be re-committed in one commit
    - MIXED:
        - `git reset --mixed <commit>`
        - discarded commits are moved into working tree
        - default, if no option is provided
        - useful for splitting one commit into multiple commits:
            - go back one commit
            - discarded commits are in working tree and can be separately re-added to staging tree
    - HARD:
        - `git reset --hard <commit>`
        - discarded commits are gone
        - useful to permanently undo commits, e.g. if feature dev did not succeed
        - useful to create new branch before resetting hard to keep changes
- undo a reset:
    - copy the hash from the discarded commit
    - after initial reset, reset branch again with `<commit>` corresponding to copied hash to go back to that point in timeline
    - only possible if no commits have been executed in-between


### Delete branch

- `git branch -d <branch>` deletes branch
- currently checked out branch cannot be deleted
- if there are unmerged commits, these will be lost when deleting
- therefore, `git branch -D <branch>` needs to be run with capital `D`


### Rename branch

- `git branch -m <name>` renames current branch to specified name
- remote-branches should not be renamed


### Checkout branch

- `git checkout <branch>` points HEAD to specified branch
- `git checkout -b <branch>` creates new branch and checks it out (`-b` stands for branch)
- `checkout` switches to branch, gets files from branch and puts them in working dir (if there are no conflicts)
- conflicts can only arise if changes have been made in the working tree
- resolve conflicts for checkout:
    - stash changes for later use
    - commit changes to clean working tree
- if no conflicts, changes are simply put in the working tree of the newly checked out branch


### Show/create branches

- `git branch` shows current branches
- currently checked out branch is marked with an asterisk
- `git branch -a` shows all branches including remotes, with option `-r` only remotes
- `git branch <name>` creates new branch with the specified name
- it matters to which branch HEAD currently points when creating new branch, because the new branch branches from this branch
- `git branch <name> <branch>` creates new branch `<name>` which branches from tip of `<branch>`
- `git branch <name> <commit>` creates new branch which branches from specified `<commit>` of current branch


## Materials

- [Tutorial](https://www.lynda.com/Git-tutorials/Git-Branches-Merges-Remotes/5030980-2.html)
