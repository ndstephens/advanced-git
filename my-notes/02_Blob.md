# # Blobs

- Git represents a file's `content` with `blobs`.
  - `blobs` are the content, not your actual files themselves.
  - `blobs` do not change (immutable), unlike `files` (mutable).
- A `blob` will not disappear from your repo as long as there is at least one file-link remaining to it.
- `blobs` are identified (and referenced) by the computed SHA1 `hash id` of its `contents`.
  - to be precise, it's the hash of some `metadata` and the `content`:
    - the object's type: "`blob`"
    - the object's `size`
    - a `\0` delimiter
    - the `content` (usually the code or text of a file)
  - this verifies the `blob`'s contents will never change (they're immutable).
  - if a file's `contents` change then a new `blob` is created.
  - identical `content` will always be represented by the same `blob`.
    - within the same repo, files that have the same content share the same `blob`.
- `blobs` are "leaf nodes" (similar to files) in `trees` (which are similar to directories).
  - multiple `trees` can reference the same `blob`.
  - different `trees` may know that `blob` as different filenames created at different times.
- `blobs` do **_NOT_** contain or reference certain information that is critical for a project, such as:
  - filenames
  - directory structures
- That information is stored in `trees`
  - `trees` know which `blobs` relate to which filenames and the directory they are stored in.

## Creating a blob

- When you add a file to the `index` a new `blob` is created.
  - `git add file.txt`
  - by that I mean you add a new file or an updated file to the "staging area".
    - it has not been committed yet
  - Remember: it's always a new `blob` being created. They are never mutated.

```sh
$ git ls-files --stage # list blobs referenced by the index
100644 ce013625030ba8dba906f756967f9e9ca394464a 0 file.txt
```

> The `index` object exists at `.git/index`. It is not a directory.

## Inspect a blob

- You first need to know or find its hash id (or at least the first 6 characters)
- `git cat-file (-t | -p) <object>` provides `content` or `type` and `size` information for repository `objects`
  - `blobs`, `trees`, and `commits` are called `objects` in git
  - they reside in `.git`'s `objects` directory

```sh
$ git cat-file -t af5626b # -t show the object type
blob
$ git cat-file -p af5626b # -p pretty-print the contents of the object
Hello, world!
```

- As can be seen, the `content` of the `blob` is simply the text.
  - can also use the `-s` flag to show its `size`
