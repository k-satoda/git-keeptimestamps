# git-keeptimestamps
A script to work around needless timestamp updates on git operations

## Motivation
If one use `git rebase` to reorder/reword/split/join..., it often
results in only timestamp updates on involved files. Such timestamp
updates trigger wasteful work if the build tool is timestamp-based one
(e.g. Make.)

In such situation, it is ideal if the timestamps are restored at the end
of `git rebase` to timestamps before the operation, provided that the
resulting file is identical to the file before the operation.

This script can be used to achieve that.

## Usage
  - git-keeptimestamps --save [--db \<dbfile>]

    Save timestamps and hash codes of all tracked files into \<dbfile>.
    If \<dbfile> is not specified, it is saved into `.git/TIMESTAMPS`.

  - git-keeptimestamps --restore [--db \<dbfile>]

    Restore timestamps of all identical (checked by hash code) files from \<dbfile>.
    If \<dbfile> is not specified, it is restored from `.git/TIMESTAMPS`.

  - git-keeptimestamps \<whatever>

    This does essentially the same as following:
    ```
    git-keeptimestamps --save
    git <whatever>
    git-keeptimestamps --restore
    ```
