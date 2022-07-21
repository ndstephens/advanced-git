# Trees

- Every `commit` holds a **_single_** `tree`.
- In order for Git to represent the structure and naming of your `files`, it attaches `blobs` as leaf nodes within a `tree`.
- A `tree` can reference other `tree`s and `blob`s.
- The `tree` is representative of the directory and file structure of your `working-tree` (project).
- You can’t discover which `tree`(s) a `blob` lives in just by looking at the `blob`, since it may have many, many owners.
  - However when you inspect a `tree`'s contents you see which `blob`s are attached to it.

## Creating a tree

- When you create a `commit` a `tree` is created.
  - The `commit` will reference the `tree`.
  - The `tree` will reference the `blobs` that were in the `index`.

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
