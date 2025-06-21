# Etc. Command

<br/>

## View Help

You can examine the functions of each command and option using the help command

```shell
# View all commands provided by Git
$ git help -all
```

```shell
# View all options available for a specific command
$ git [command] -help
```

<br/>

## Setup and Initialization

Initialize a Repository or clone an existing Repository

```shell
# Create a Git repository based on the current directory
$ git init
```

```shell
# Clone a remote Repository to a local Repository through URL
$ git clone [url]
```

<br/>

## Stage & Commit

You can commit using the stage area

```shell
# Check modified files in the current directory for the next commit
$ git status
```

```shell
# Add files for the next commit (stage)
$ git add [file]
```

```shell
# Unstage added files: changes are maintained
$ git reset [file]
```

```shell
# Show unstaged changes
$ git diff
```

```shell
# Show changes that are staged but not committed
$ git diff --staged
```

```shell
# Commit staged content with a message (create snapshot)
$ git commit -m "[descriptive message]"
```

<br/>

## Comparison and Inspection

You can inspect logs and changes

```shell
# Show all commit history of branchA that's not in branchB
$ git log branchB..branchA
```

```shell
# Display all commits containing changes to that file (also shows file name changes)
$ git log --follow [file]
```

```shell
# Show the change content (diff) of what's in branchA but not in branchB (compare states between branches)
$ git diff branchB...branchA
```

<br/>

## Share and Update

You can search for updates in a specific Repository and update the local Repository

```shell
# Add a specific remote Repository through url with an alias
$ git remote add [alias] [url]
```

```shell
# Fetch all branches and data from the remote Repository added with an alias to local
$ git fetch [alias]
```

```shell
# Merge the remote branch with the currently working branch to make it up to date
$ git merge [alias]/[branch]
```

```shell
# Send commits from the local branch to the remote branch
$ git push [alias] [branch]
```

```shell
# Fetch information from the remote Repository and automatically merge it into the local branch
$ git pull
```

<br/>

## History Modification

You can modify branches or commits or delete commit history

```shell
# Apply commits after a specific branch's fork to the currently working branch
$ git rebase [branch]
```

```shell
# Go back to before a specific commit and erase all staged changes
$ git reset --hard [commitish]
```

<br/>

## Temporary Storage

You can temporarily store modified or tracked files to switch branches

```shell
# Temporarily store modified or staged changes on the stack and remove them from current work history
$ git stash
```

```shell
# Show a list of changes temporarily stored on the stack
$ git stash list
```

```shell
# Apply changes temporarily stored on the stack back to the current work history
$ git stash apply
```

```shell
# Apply changes temporarily stored on the stack back to the current work history and delete from the stack
$ git stash pop
```

```shell
# Delete changes temporarily stored on the stack
$ git stash drop
```
