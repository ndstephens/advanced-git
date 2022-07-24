# Commits

- A `commit` is a code snapshot...what the project looked like at that point in time.
  - It's a combination of the changes from the `index` (staging area) and the previous `commit`.
- Every `commit` points to a **_single_** `tree`.
- A `commit` will have a SHA-1 `hash id` created by its content and metadata:
  - the object's type: "`commit`"
  - the object's `size`
  - the `author` and `committer` (usually the same person)
  - the `date`
  - the `message`
  - pointers to one or more `parent commits` (their `hash-id`'s)
  - the `content` (its pointer to a `tree`)
    - that `tree` is a snapshot of the repo at the time of the commit.
    - that `tree` points at files and directories.
- You can never change or update a `commit`, only create a new one.
  - Even if the `contents` don't change, the `created date` will...which will cause the hash-id to be different.
  - This keeps your commit history secure and prevents data corruption.
- Every `commit` has **_at least_** one `parent commit` (other than the initial commit), and those `parent commits` will have `parents`.
  - This is what allows a single `commit` to be treated like a `branch`: because it knows the whole history that led up to it.
- To Git...**_the world is simply a collection of `commit` `objects`, each of which points to a `tree` that points to other `trees` and `blobs`, which store your data. Anything more complicated than this is simply a device of nomenclature._**

---

## Commits by name

- All `commit` objects are structurally the same...`names` are just used for `referencing` a specific `commit`.
- Also see ["A commit by any other name"](https://jwiegley.github.io/git-from-the-bottom-up/1-Repository/6-a-commit-by-any-other-name.html)

### \- Branch

- A `branch` is nothing more than a `named reference` to a `commit`.
- It will also be the `head`, or most recent, `commit` in a **_lineage_** of `commits` which define a history of work.
- It's updated every time a new commit is added to that that lineage.

### \- Tag

- A `tag` is a `named reference` to a **_specific_** commit.
- Will always be linked to the exact same commit. It **_does not change_** like `branch`.
- `tags` can have descriptions.

### \- HEAD

- Refers to whichever `commit` is currently `checked out`.
- Usually that's a `branch`.
- If not a `branch` then it's called a `detached HEAD`.

---

## Other commit terminology

### \- Merge

- A commit that has multiple parents.

### \- Ancestor (or start) of a branch

- A commit that has multiple children.

---

## Creating a commit

- When you run the `git commit` command.
  - A new `tree` is created.
  - A `commit` object is created to hold the tree.
  - The `blobs` currently in the `index` are contained in that tree.
  - The `commit` is linked to a `parent commit`(s)
- Commits will be registered as the new `head` of a `branch` when they're created.

---

## Inspect a commit

- You can examine all the top-level, referenced `commits` at any time using the `git branch` command (since all `branches` are just a `named reference` to a `commit`):

```sh
$ git branch -v
* master 5f1bc85 Initial commit
```

- To inspect the `commit object` can use `git cat-file -p <name | commit-hash-id>`:

```sh
$ git cat-file -p HEAD # HEAD - reference the most recent commit of the branch you're checked out
tree 4cf9f177c4c015836fca6a31f9c3917e89ae29ec # the tree
author Nate Stephens <myemail@github.com> 1658409908 -0400
committer Nate Stephens <myemail@github.com> 1658409908 -0400

Initial commit # the commit message
```

- To show the `commit` contents use `git show <name | commit-hash-id>`:

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
