# Trees

- A `tree` contains pointers to `blobs` and other `trees`.
  - `blobs` relate to files
  - `trees` relate to directories
- A `tree` will have a SHA-1 `hash id` created by its content and metadata:
  - the object's type: "`tree`"
  - the object's `size`
  - a `\0` delimiter
  - the `content` (its pointers to `blobs` and other `trees`)
    - each pointer lists:
      - its `type` (`blob` or `tree`)
      - the `hash-id` of that `blob` or `tree`
      - the filename or directory name associated with that `blob` or `tree` (remember that multiple files can point to the same `blob`)
      - the file or directory's mode (executable, symbolic link, ...)
- When you inspect a `tree`'s contents you see which `blobs` and `trees` it points to.
- The `tree` and its `hash id` are forever linked, and the `tree` is immutable.
- Two `tree`'s with identical contents would have the same `hash id` (just like with `blob`s).
- Every `commit` holds a **_single_** `tree`.
  - but again...that `tree` can point to other `trees` (similar to sub-directories)

---

## Creating a tree

- When you create a `commit` a `tree` is created.
  - The `commit` will reference the `tree`'s hash id.
  - The `tree` will reference the `blobs` that were in the `index` (the staging area).

---

## Inspect a tree

- You'll need to find the hash id that references the `tree`, or know the `commit` the `tree` belongs to.
- Since `tree`s are owned by `commit`s, it usually easiest to get the `commit`'s hash id (or name) that has the `tree` you're looking for.
  - often times, that might be the `HEAD`.
  - `HEAD` is just a named referenced to a `commit`, so you can use it instead of the hash id.
- To inspect a `commit object` can use `git cat-file -p <name | commit-hash-id>`:

```sh
$ git cat-file -p HEAD # HEAD reference the most recent commit of the branch you're checked out
tree 4cf9f177c4c015836fca6a31f9c3917e89ae29ec # the tree
author Nate Stephens <myemail@github.com> 1658409908 -0400
committer Nate Stephens <myemail@github.com> 1658409908 -0400

Initial commit # the commit message
```

- You now have the `tree`'s hash id (4cf9f1...)
- Once you have the `tree` hash id you have two options to view the `tree` object:

```sh
$ git cat-file -p 4cf9f1 # <tree-hash-id>
100644 blob ce013625030ba8dba906f756967f9e9ca394464a	file.txt

# Can also use the `-r` flag to show the `tree` object recursively
```

- As a shortcut you can also use the `git ls-tree <tree-ish>` command and provide it either the `commit` or `tree` hash id (or a commit's named reference such as `HEAD`):

```sh
$ git ls-tree HEAD # <commit-name | commit-hash-id | tree-hash-id>
100644 blob ce013625030ba8dba906f756967f9e9ca394464a	file.txt
```

- The `100644` number is the file mode (permissions)
  - The first three digits are for the executable status for the user, group, and other.
    - `1` - executable permission
    - `0` - not executable
  - The last three digits are for the read-wrote status for the user, group, and other.
    - `6` - read and write permissions
    - `4` - read only
    - `2` - write only
    - `0` - none
