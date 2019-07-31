# Branch


- for each new big feature, create a new branch
- if feature development succeeds, merge feature-branch into master-branch
- useful for isolating these features separate from dev on master
- each branch accesses the same un-staged changes, but has its own staging tree and repo


### Reset branch

- `reset` changes the files in the staging tree and/or working tree to the state they had when a specified commit was made 
- moves HEAD to the specified commit and previous commits will be discarded
- "Make my project look like it did back then"
- Careful if commits are already shared with remote
- Mostly used within private repo and when changes are not pushed to remote, yet


- 3 reset types:
    - SOFT:
        - `git reset --soft <commit>`
        - e.g. with `<commit> =  HEAD^` latest commit is discarded and HEAD points to last but one
        - discarded commits are moved into staging tree
        - useful for making one commit out of two:
            - go back two commits with `<commit> = HEAD^^`
            - discarded commits are in staging tree and can be re-committed in one commit
    - MIXED:
        - `git reset --mixed <commit>`
        - discarded commits are moved into working tree
        - default, if no option is provided
        - useful for splitting one commit into multiple commits:
            - go back one commit
            - discarded commits are in working tree and can be re-added to staging tree
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
- `checkout` switches to branch, gets files from branch and puts them in working tree, if there are no conflicts
- `__git_ps1` starts script showing current branch in console


### Show/create branches

- `git branch` shows current branches
- currently checked out branch is marked with an asterisk
- `git branch -a` shows all branches including remotes, with option `-r` only remotes
- `git branch <name>` creates new branch with the specified name
- `git branch <name> <branch>` creates new branch which branches from `<branch>`


- it matters to which branch HEAD currently points when creating new branch, because the new branch branches from this branch


## Materials

- [Tutorial](https://www.lynda.com/Git-tutorials/Git-Branches-Merges-Remotes/5030980-2.html)
