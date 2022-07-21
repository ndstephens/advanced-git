# Terminology

> Many of the definitions came from the site [Git from the Bottom Up](https://jwiegley.github.io/git-from-the-bottom-up/)

### `.git` directory example (the "repository"):

- after the initial commit of one file

```
├── COMMIT_EDITMSG
├── HEAD
├── config
├── description
├── hooks
│   └── <etc>.sample
├── index
├── info
│   └── exclude
├── logs
│   ├── HEAD
│   └── refs
│       └── heads
│           └── main
├── objects
│   ├── 4c
│   │   └── f9f177c4c015836fca6a31f9c3917e89ae29ec <-- tree
│   ├── c9
│   │   └── fc41d8dce46b0674afbe18601c51c2e11798a0 <-- commit
│   ├── ce
│   │   └── 013625030ba8dba906f756967f9e9ca394464a <-- blob
│   ├── info
│   └── pack
└── refs
    ├── heads
    │   └── main
    └── tags
```

## Repository - the `.git` directory and its contents

- A collection of `commits`, each of which is an archive of what the project’s `working tree` looked like at a past date, whether on your machine or someone else’s.
- It also defines `HEAD`, which identifies the branch or commit the current `working tree` stemmed from.
- Lastly, it contains a set of `branches` and `tags`, to identify certain `commits` by name.

## Index - the "staging area"

- Git does not commit changes directly from the `working tree` into the `repository`.
- Instead, changes are first registered in something called the `index`.
- Think of it as a way of “confirming” your changes, one by one, before doing a `commit` (which records all your approved changes at once).

## Working Tree - your project directory

- Any directory on your filesystem which has a `repository` associated with it (typically indicated by the presence of a sub-directory within it named `.git`).
- It includes all the files and sub-directories in that directory.
- Git maintains **_snapshots_** (aka `commit`s) of a directory's contents.
  - that directory is your `working tree` (aka your project).
  - this concept is the basic task of git.

## Commit

- A **_snapshot_** of your `working tree` at some point in time.
- The state of `HEAD` at the time your `commit` is made becomes that commit’s parent.
  - This is what creates the notion of a “revision history”.

## Branch

- Just a **_name_** for a `commit`, also called a `reference`.
- It’s the **_parentage_** of a `commit` which defines its history, and thus the typical notion of a “branch of development”.
- It's the `alias` for a specific `commit` that changes every time you add a new `commit` to a "branch" (or chain of commits).
  - Refers to the most recent `commit` in that "branch"
  - Can also be thought of as the head of that chain of commits.
  - When you're on that branch, `HEAD` and `branch` reference the same `commit`.
  - When you make a new `commit`, they both then change to reference that new `commit`.
  - `branch` will continue to reference that same `commit` even after you `checkout` another `branch` or `commit`.

## Tag

- Also a name for a `commit`, similar to a `branch`, except that it always names the same `commit`, and can have its own **_description text_**.
- The `tag` will always continue to `reference` that exact same `commit` it was originally assigned to.

## Main - (used to be master)

- The mainline of development in most `repositories` is done on a branch called `main`.
- Although this is a typical default, it is in no way special.

## HEAD

- Used by your repository to define what is currently checked out:
- If you `checkout` a `branch`, `HEAD` symbolically refers to that `branch`, indicating that the `branch` name should be updated after the next `commit` operation.
- If you `checkout` a specific `commit`, `HEAD` refers to that `commit` only. This is referred to as a `detached HEAD`, and occurs, for example, if you check out a `tag` name.
  - If `HEAD` doesn't refer to a `branch` then it's a `detached HEAD`.
