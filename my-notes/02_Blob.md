# # Blobs

- Git represents your file's `contents` with `blobs`.
  - `blobs` are content, not files.
  - `blobs` do not change (immutable), unlike `files` (mutable).
  - they store no `metadata` about the content.
  - `metadata` is kept in the `tree` that holds the `blob`.
- `blobs` are "leaf nodes" in `trees` (similar to directories).
  - multiple `trees` can reference the same `blob`.
  - different `trees` may know that `blob` (those contents) as different files created at different times.
- `blobs` are named by computing the `SHA1` hash id of its `size` and `contents`.
  - they have no proper "name" nor structure.
    - simply referenced by the SHA1 that is determined by their specific content.
  - this verifies the `blob`'s contents will never change (they're immutable).
  - identical content will always be represented by the same `blob` (SHA1).
    - therefore, identical content will **_NOT_** create a new `blob` but instead **_share_** a previously created `blob` within the same repo.
- Will not disappear from your repo as long as there is at least one file-link remaining to it.

## Creating a blob

- When you add a file to the `index` a new `blob` is created.
  - by that I mean you add a new file or an updated file to the "staging area".
    - it has not been committed yet. That isn't required to create a `blob`.
  - and remember, it's always a new `blob` being created. They are never mutated.

## Inspect a blob

- You first need to know or find its SHA1 (or at least the first 6 characters)
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
