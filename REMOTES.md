# Remotes

- branch `origin/master` is stored locally, mirrors master-branch on local machine and references remote-master-branch
- `origin/master` is the tracking branch for the remote-branch and tries to stay always in sync with its remote
- generally, commit locally, fetch remote to `origin/master`, merge local commits with `origin/master` and push results to remote
- remote-tracking-branches cannot be checked out
- multiple remote-branches can be added


### Pull from remote

- `git pull` does both steps fetching and merging, at once
- if no local changes have been made, `pull` recommended
- otherwise, `fetch` for more fine-grained control about merge conflicts


### Fetch from remote

- `git fetch <remote>` synchronizes `origin/<remote>` with its remote
- if only one remote and due to tracking, `<remote>` can be omitted
- generally, fetch often and fetch before each push
- `fetch` saves changes from remote only to local tracking-branch `origin/master`, but changes are not merged into `master`, yet
- therefore, `git merge origin/master` executed from `master` to merge `origin/master` into `master`


### Clone repo

- `git clone <url> <dir>` clones remote to `<dir>`
- if `<dir>` does not exist, directory is created
- if `<dir>` not provided, repo is stored in subdirectory with name equivalent to remote-branch
- `clone` provides access to all pushed remote-branches and adds tracking automatically


### Push to remote

- `git push -u origin master` pushes `master`-branch to `origin`-remote (alias) and  moves the `origin/master`-pointer to be in sync with `master`
- consequently, the corresponding branch `master` in remote `origin` and local `origin/master` are in sync
- `-u` ensures that local `origin/master` tracks remote and stands for 'upstream'
- allows not to explicitly mention remote-branch each time for fetching, pulling and pushing
- for following pushes, `-u`-option can be omitted since tracking is already initiated
- consequently `origin master` can also be omitted ->  `git push`
- `pull` (or `fetch` and `merge`) before `push` to make sure local `master` is in-sync with remote and integration succeeds


### Create local tracking branch

- e.g. if additional remote-branches have been pushed in the meantime
- `git checkout -b <branch> origin/<remote>` creates new branch `<branch>` which branches off the remote-tracking branch `origin/<remote>` and checks it out
- enables to work on that remote-branch


### Delete remote branch

- `git push origin --delete <branch>` deletes remote-`<branch>` from remote `origin` and tracking branch


### Add remote branch

- `git push -u origin <branch>` pushes local `<branch>` to remote and also enables tracking


### Add remote to local repo

- `git remote add origin <url>` and `git push -u origin master`
- `origin` is standard name of remote-alias
- `git remote -v` shows remotes
- remote-metadata is stored in `.git/config`
- `git remote rm origin` would delete remote-branch `origin`


## Materials

- [Tutorial](https://www.lynda.com/Git-tutorials/Git-Branches-Merges-Remotes/5030980-2.html)
