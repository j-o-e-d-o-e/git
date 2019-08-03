# Patches

- share changes via files
- useful when changes are not ready for a public branch, e.g. during a review/approval process
- files can then be shared via email, ext drive etc.


### Create formatted patches

- formats diff-patches in Unix-mailbox format 
- `git format-patch <commit>..<commit>` exports all commits in the range of the specified commits in separate formatted files
- if a `<commit>` is omitted, git uses the current HEAD as the second `<commit>`, by default
- option `-o <dir>` specifies directory where to store patches
- `git format-patch -1 <commit>` exports a single commit


### Apply formatted patches

- extracts author, commit message, and changes form mailbox-message and applies them to the current branch
- unlike diff patch, changes *are not* applied to the working tree and commit history *is* transferred, i.e. commits are saved as new commits
- `git am <patch>` applies specified patch, e.g. `git am ~/Desktop/patches/*.patch`


### Create diff patches

- `git diff HEAD^^ HEAD > <file>.diff` creates diff path which contains differences between last but one and current commit and stores it in `<file>`
- `<file>.diff` stands for the abs file path, e.g. `~/Desktop.review.diff`
- `HEAD` can be omitted, git then generates difference to current commit to which HEAD points, by default


### Apply diff patches

- `git apply <diff-patch>` applies changes in the specified `<diff-path>` file to the working tree
- only changes, no commit history is transferred
- works best if patched changes are not additional, but only apply to already existing elements


## Materials

- [Tutorial](https://www.lynda.com/Git-tutorials/GIT-Intermediate-Techniques/664821-2.html)