# git restore, revert, reset

<br/>

## git restore : Revert a single file

Revert current file modifications to the most recently committed state

```shell
git restore filename
```

Restore the entered file to a specific commit ID point

```shell
git restore --source commit_id filename
```

Unstage a specific file

```shell
git restore --staged filename
```

<br/>

## git revert : Revert a commit

If you want to cancel past commit history, it creates an additional commit that cancels one commit. In other words, it's a command that can erase what was done in a specific commit.

```shell
git revert commit_id
```

![git_revert](/Images/git_revert.png)

- If vim editor appears, modify the commit message and close it
- When reverting, you can enter multiple commit IDs simultaneously
- To revert only the most recent commit: enter git revert HEAD
- Commits newly created by merge commands can also be reverted

<br/>

## git reset : If you want to revert everything

You can completely revert everything to a specific commit (including files in working directory)

```shell
git reset --hard commit_id
```

![git_reset](/Images/git_reset.png)

- However, **you must be very careful when using it in collaborative projects**
- Untracked files (files not added with git add) are not deleted and remain
- git clean command can delete all untracked files (more dangerous..)
- If you want to review and commit again (while unstaging) instead of completely deleting files during reset, use `--soft` or `--mixed` instead of `--hard`
- Of course, when you enter `git reset`, the `--mixed` option works by default, and only the index (Staging Area) is reset.
