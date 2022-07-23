# Git

## What is Git?

Git is a distributed version control system.

## How does it store information?

At its core, `git` is like a `key-value` store.

- `Key` - hash of the `data`
- `Value` - the `data`

You use the `key` to reference the `content` (aka value or data).

Git calls these `key-value` pairs `objects`.

## What is an Object

There are 3 main `types` of `objects`:

- `blobs`
- `trees`
- `commits`

Git stores `objects` in the `.git/objects` directory.

Each `object` contains the `hash-id` (the key) and the `content` (the value) it references.

## How do you create a key?

You use a cryptographic `hash function` (known as `SHA-1`) which takes an `input` and produces a 160-bit hash value (known as a "message digest") rendered as a `hexadecimal number, 40 digits long`.

- Given a piece of data, it outputs a 40-digit hex number.
  - Given the same data, it outputs the same number
- We call that number the `hash id`.
- The `hash id` will always be the same if the given input is the same.
- This is known as a **_content addressable storage system_**.
  - That's because it is the content itself that generates the specific key.

## Why use this type of key?

- Revision control systems such as Git use SHA-1 not for security, but to identify revisions and to ensure that the data has not changed due to accidental corruption.
- It's purely a consistency check.
- You can verify that the data you get back out is the exact same data you put in.
