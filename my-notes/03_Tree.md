# Trees

- Every `commit` holds a **_single_** `tree`.
- A `tree` will contain `blob`'s and can also contain other sub-`tree`s
- The `tree` represents the directory and file structure of your `working-tree` (project).
- You can’t discover which `tree`(s) a `blob` lives in just by looking at the `blob`, since it may have many, many owners.
  - However when you inspect a `tree`'s contents you see which `blob`s are attached to it.
- A `tree` will have a SHA1 hash id created by its contents (just like a `blob`).
  - The `tree` and its hash id are forever linked, and the `tree` is immutable.
  - Two `tree`'s with identical contents would have the same hash id (just like `blob`s).

## Creating a tree

- When you create a `commit` a `tree` is created.
  - The `commit` will reference the `tree`'s hash id.
  - The `tree` will reference the `blobs` that were in the `index` (the staging area).

## Inspect a tree

- You'll need to find the hash id that references the `tree`, or know the `commit` the `tree` belongs to.
- Since `tree`s are owned by `commit`s, it usually easiest to get the `commit`'s hash id that has the `tree` you're looking for.
  - often times, that might be the `HEAD`.
  - `HEAD` is just a named referenced to a `commit`, so you can use it instead of the hash id.

```sh
$ git cat-file -p HEAD # HEAD reference the most recent commit of the branch you're checked out
tree 4cf9f177c4c015836fca6a31f9c3917e89ae29ec # the tree
author Nate Stephens <myemail@github.com> 1658409908 -0400
committer Nate Stephens <myemail@github.com> 1658409908 -0400

Initial commit # the commit message
```

> This is showing the contents of the `commit` object.

- You now have the `tree`'s hash id (4cf9f1...)
- As a shortcut you can also use the `git ls-tree <tree-ish>` command and provide it either the `commit` or `tree` hash id (or a commit's named reference such as `HEAD`):

```sh
$ git ls-tree HEAD
100644 blob ce013625030ba8dba906f756967f9e9ca394464a	file.txt
```

- If you have the `tree` hash id you have two options to view the `tree` object:

```sh
$ git cat-file -p 4cf9f1 # or "git ls-tree 4cf9f1"
100644 blob ce013625030ba8dba906f756967f9e9ca394464a	file.txt
```

> If using `cat-file` with `HEAD` or a `commit`'s hash id then it will return the `commit` object.
>
> Can also use the `-r` to show the `tree` object recursively
