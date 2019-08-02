# Intermediate Techniques


### Cherry-pick commits

- apply the changes from one or more existing commits
- each cherry-picked commit becomes a new commit on the current branch
- but, the hash of these new commits differs from the hash of the cherry-picked commit, since its parent-commit and metadata differs
- useful for copying a specific change/commit from another branch instead of merging branches and getting all changes


- `git cherry-pick <commit>` copies specified commit (e.g. hash or tag) into current branch and creates new commit
- commit message is by default equal to the original message of the cherry-picked commit
- with option `-e` a new commit message can be edited


- commits which are merge-commits cannot be cherry-picked
- cherry-picking can result in conflicts to be resolved


### Force push

- if local state is preferable to remote state, e.g. if remote went wrong and needs repair
- `git push -f` forces push and replaces remote state with local state


- scenario might be:
    - `git fetch` fetches changes from remote
    - inspection of changes shows these are undesirable
    - discuss changes with project collaborators and announce force push 
    - force push to discard these changes and add local changes
    - all other collaborators need to pull changes and then perform `git reset --hard origin/master` to sync correctly
- use with extreme caution, since disruptive change


### Prune stale remote-tracking branches

- delete abandoned remote-tracking branches which no longer tracks a remote-branch because the remote-branch has been deleted
- if one deletes remote-branch, remote-tracking branch is automatically deleted
- but, when collaborators delete remote-branch, one has to delete the remote-tracking branch on one's own machine
- `git remote prune origin` deletes stale remote-tracking branches


---

### Interactive staging

- allows staging portions of changed files and to make smaller, more focused commits
- `git add -i` enters interactive staging mode in console
- from there, patch mode for partial stages ('hunks') can be entered


### Bisect

- to find a commit which introduced a bug or regression
- in a bisect-session, search-space is continuously narrowed to identify the bad commit

- procedure:
    - `git bisect start` starts bisect-session
    - `git bisect bad <commit>` marks `<commit>` as bad.
    - if `<commit>`omitted, it will where HEAD currently points to, by default
    - `git bisect good <commit>` marks `<commit>` as good
    - the mid-point is loaded in the working tree and HEAD points to this mid-point
    - one checks this state to define if it is good or bad, e.g. by running tests or manually 
    - `git bisect good` or `git bisect bad` marks again the current mid-point
    - bisect proceeds by moving HEAD to the new mid-point and loading the new state in working tree
    - checking and marking can be repeated multiple times until bisect narrows possibilities down to one commit
    - finally, `git bisect reset` exits bisect and resets working tree to where HEAD pointed before bisect-session
    - one has identified the bad commit and can take further actions...


### Blame

- `git blame <file>` lists changes in `<file>` line by line with metadata and to which commit these changes belong
- with option `-w` whitespace is ignored
- `git blame -L <start>,<end> <file>` list changes in `<file>` from line `<start>` to `<end>`
- `git blame <commit> <file>` list changes in `<file>` in the timeline up to `<commit>`
- useful to check who made which changes and when and why


### Log options

- `git log -p` lists commits as patches/diffs
- `git log -L <start>,<end>:<file>` lists changes in `<file>` from line `<start>` to `<end>`


## Materials

- [Tutorial](https://www.lynda.com/Git-tutorials/GIT-Intermediate-Techniques/664821-2.html)