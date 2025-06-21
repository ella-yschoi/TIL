# git merge, rebase

<br/>

## git merge

### 3-way-merge

![git_merge](/Images/git_merge.png)

When each branch has one or more new commits, if you run the git merge command, it automatically creates a new commit by combining the code from both branches → basic operation method of merge

### fast-forward merge

![git_fast_forward_merge](/Images/git_fast_forward_merge.png)

Sometimes there are commits only in the new branch and **no new commits in the base branch**, when you merge, it's called "fast-forward merge".
This means there's nothing to merge, so it tells the new branch "from now on you are the main branch". Of course, the result is the same as 3-way merge

<br/>

## git rebase & merge

![git_rebase](/Images/git_rebase.png)

Moving the starting point of a branch to another commit
Move the starting point of the new branch to the latest commit of the main branch using rebase, then do fast-forward merge

```shell
git switch {new branch}
git rebase main

git switch main
git merge {new branch}
```

<br/>

## git squash & merge

![git_squash](/Images/git_squash.png)

Stage files to be committed by moving them from working directory to staging area

```shell
git switch main
git merge --squash {branch name}
git commit -m 'message'
```
