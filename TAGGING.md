# Tagging


### Check out tags

- `git checkout -b <branch> <tag>` creates new branch `<branch>` which branches off commit referenced by `<tag>` and checks it out
- `git checkout <tag>` checks out specified tag, but leads to un-preferred 'detached HEAD' state


### Push tags to remote

- like branches, tags are local unless shared to a remote
- `git push` does not push tags
- but, `git fetch` automatically retrieves shared tags
- `git push origin <tag>` pushes `<tag>` to the remote `<origin>`
- `git push origin --tags` pushes all tags to the remote


### Delete tags

- `git tag -d <tag>` deletes `<tag>`
- `git push -d origin <tag>` deletes a shared tag `<tag>` on the remote `origin`
- does not delete referenced commits, only the tags


### Create tags

- tags allow marking points in the timeline as important, a named reference to a commit
- instead of a hash, tags can then be used, e.g. `git show <tag>` shows commit tagged with `<tag>`


- `git tag -a <tag> -m "message" <commit>` creates tag with specified name for specified commit (hash or `HEAD`) with a message
- `-a` stands for annotated tag
- if message not provided in command, git opens editor for multiline message
- if `<commit>`-hash not provided, the latest commit/current HEAD is tagged by default
- e.g. `git tag -am "Start" v0.0` creates annotated tag 'v0.0' for HEAD with the message 'Start'


- `git tag` lists all current tags, optional with option `-l`
- with option `-n` shows additionally the annotations


## Materials

- [Tutorial](https://www.lynda.com/Git-tutorials/GIT-Intermediate-Techniques/664821-2.html)