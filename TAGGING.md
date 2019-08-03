# Tagging

- tags allow to mark commits as important, a named reference to a commit
- tags can then be used to declare a commit instead of a hash

### Create tag

- `git tag -a <tag> -m "<message>" <commit>` creates a tag with the name `<tag>` for `<commit>` and a `<message>`
- `-a` stands for 'annotated tag'
- if message is not provided in command, git opens editor for multi-line message
- if `<commit>` not provided, the latest commit where HEAD points to is tagged by default
- e.g. `git tag -am "Start" v0.0` creates annotated tag 'v0.0' for HEAD with the message 'Start'


### Show tag

- `git show <tag>` shows the commit tagged with `<tag>`
- `git tag` lists all current tags, with option `-n` shows also the annotations


### Check out tag

- `git checkout -b <branch> <tag>` creates new branch `<branch>` which branches off commit referenced by `<tag>` and checks it out
- `git checkout <tag>` checks out specified tag, but leads to un-preferred 'detached HEAD' state


### Push tag to remote

- `git push` does not push tags
- but, `git fetch` automatically retrieves shared tags
- `git push origin <tag>` pushes `<tag>` to the remote `<origin>`
- `git push origin --tags` pushes all tags to the remote


### Delete tag

- `git tag -d <tag>` deletes `<tag>`
- `git push -d origin <tag>` deletes a shared tag `<tag>` on the remote `origin`
- does not delete the referenced commits, only the tags


## Materials

- [Tutorial](https://www.lynda.com/Git-tutorials/GIT-Intermediate-Techniques/664821-2.html)