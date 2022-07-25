# Three Areas Where Code Lives

## Working Area (aka "working tree")

- All the files and folders that we add to the Git repository are known as the Git working tree.
  - The .git folder is not a part of the working tree.
- This working tree tracks the files, folders, and the changes that we make inside them.
- A working tree in a Git Repository is the collection of files which are originated from a certain version (a commit) of the repository.

## Staging Area (aka "index" or "cache")

- Will be included in the next commit.
- The staging area is how git knows what will change between the current current and the next commit.

## Repository

- Everything in your .git directory.
- The files git knows about (b/c they've been committed at one point).
- Contains all your commits.
