# Commits

- Every `commit` holds a **_single_** `tree`.
- A `commit` will have a SHA1 hash id created by its contents.
  - Unlike a `tree` or `blob`, no two `commit` objects will ever have the same hash id.
  - That's b/c `commit` objects refers to both your name, and the date at which you created the commit, as well as their content (the tree and blobs).
    - The date alone will always cause a `commit` hash to be different, regardless of the other content.
- Every `commit` has at least one `parent commit` (other than the initial commit), and those `commits` will have `parents`.
  - This is what allows a single `commit` to be treated like a `branch`: because it knows the whole history that led up to it.
- To Git **_the world is simply a collection of `commit` `objects`, each of which holds a `tree` that references other `trees` and `blobs`, which store your data. Anything more complicated than this is simply a device of nomenclature._**

## Commits by name

- All commits are basically the same...names are just for referencing
- Also see ["A commit by any other name"](https://jwiegley.github.io/git-from-the-bottom-up/1-Repository/6-a-commit-by-any-other-name.html)

### \- Branch

- A `branch` is nothing more than a `named reference` to a `commit`.
- It will also be the `head`, or most recent, `commit` in a **_lineage_** of `commits` which define a history of work.
- It's updated every time a new commit is added to that that lineage.

### \- Tag

- A `named reference` for a specific commit.
- Will always be linked to the exact same commit. It doesn't change like `branch`.
- `tags` can have their descriptions.

### \- HEAD

- Refers to whichever `commit` is currently `checked out`.
- Usually that's a `branch`.
- If not a `branch` then it's called a `detached HEAD`.

## Other commit terminology

### \- Merge

- A commit that has multiple parents.

### \- Ancestor of a branch

- A commit that has multiple children.

## Creating a commit

- When you run the `git commit` command.
  - A new `tree` is created.
  - A `commit` object is created to hold the tree.
  - The `blobs` currently in the `index` are contained in that tree.
  - The `commit` is linked to a `parent commit`(s)
- Commits will be registered as the new `head` of a `branch` when they're created.

## Inspect a commit

- You can examine all the top-level, referenced `commits` at any time using the `branch` command (since all `branches` are just a `named reference` to a `commit`):

```sh
$ git branch -v
* master 5f1bc85 Initial commit
```

- To inspect the `commit object`:

```sh
$ git cat-file -p HEAD <or-hash-id> # HEAD - reference the most recent commit of the branch you're checked out
tree 4cf9f177c4c015836fca6a31f9c3917e89ae29ec # the tree
author Nate Stephens <myemail@github.com> 1658409908 -0400
committer Nate Stephens <myemail@github.com> 1658409908 -0400

Initial commit # the commit message
```

- To show the `commit` contents:

```sh
$ git show HEAD
Author: Nate Stephens <myemail@github.com>
Date:   Thu Jul 21 09:25:08 2022 -0400

    commit file.txt

diff --git a/file.txt b/file.txt
new file mode 100644
index 0000000..ce01362
--- /dev/null
+++ b/file.txt
@@ -0,0 +1 @@
+Hello, world!
```
