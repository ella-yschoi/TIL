# git add, commit

<br/>

## Using git in working directory

- When you enter the command to create a new Git repository, a Git repository is created based on the current directory.

  ```shell
  git init
  ```

<br/>

## Creating versions by adding and committing

- Stage files to be committed by moving them from working directory to staging area

  ```shell
  git add filename
  ```

- Stage multiple files

  ```shell
  git add filename1 filename2
  ```

- Stage all files

  ```shell
  git add .
  ```

- If you want to know about currently changed files and staged files, enter the command below

  ```shell
  git status
  ```

- If you want to remove files from staging area, enter the command below

  ```shell
  git restore --staged filename
  ```

- Move from staging area to repository

  ```shell
  git commit -m 'write commit message'
  ```

- If you want to see commit history at a glance, enter the command below

  ```shell
  # Show as text
  # After entering, if Vim editor opens, you can scroll up/down with j, k keys, and exit with q key
  git log
  ```

  ```shell
  # Show as graph
  # After entering, if Vim editor opens, you can scroll up/down with j, k keys, and exit with q key
  git log --graph
  ```

- Cancel commit

  ```shell
    # [Method 1] Cancel commit and preserve files in staged state in working directory
    git reset --soft HEAD^

    # [Method 2] Cancel commit and preserve files in unstaged state in working directory
    # Default option
    git reset --mixed HEAD^
    # Same as above
    git reset HEAD^
    # Cancel last 2 commits
    git reset HEAD~2

    # [Method 3] Cancel commit and delete files from working directory in unstaged state
    git reset --hard HEAD^
    git-cancel.html
  ```
