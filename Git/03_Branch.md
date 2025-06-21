# git branch

<br/>

## branch commands

### check branch

```shell
# You can check the currently working branch with * mark
git branch
```

### create branch and switch to it

```shell
git branch {branch name to create}
```

```shell
git checkout -b {branch name to create}
```

```shell
git switch -c {branch name to create}
```

### move branch

```shell
git checkout {branch name to move to}
```

```shell
git switch {branch name to move to}
```

### merge branch

```shell
  # Switch to main branch for merge
  git switch main

  # Merge feat/todo branch into main branch
  git merge feat/todo
```

However, in actual project development, rather than merging branches locally, it's more common to use GitHub's pull request feature to thoroughly review changes before merging, so it's recommended to push the feature branch and request a PR instead of merging locally

```shell
  # Push to GitHub repository
  git push origin feat/todo
  # Pull Request and merge on GitHub
```

### delete branch

```shell
# Delete merged branch
git branch -d {branch name to delete}

# Delete unmerged branch
git branch -D {branch name to delete}
```

<br/>

## branch related errors

- When trying to delete a branch, the following error may occur. This is an error that occurs because the **changes made in the branch are not merged**. If the changes aren't particularly important, you can force delete the branch by entering `git branch -D`.

  ```shell
  error: The branch 'branchname'isnot fully merged.
  If you are sure you want todelete it, run 'git branch -D branchname'.
  ```

- However, the above force deletion only deletes the branch locally, so you also need to delete the branch on the remote server.
