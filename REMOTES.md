# Remotes

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


## Materials

- [Tutorial](https://www.lynda.com/Git-tutorials/Git-Branches-Merges-Remotes/5030980-2.html)
