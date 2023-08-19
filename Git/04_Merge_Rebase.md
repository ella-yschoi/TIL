# git merge, rebase

> Reference: codingapple

## git merge

### 3-way-merge

![git_merge](/Images/git_merge.png)

브랜치에 각각 신규 commit이 1회 이상 있는 경우, git merge 명령을 내리면 두 브랜치의 코드를 합쳐서 새로운 commit을 자동으로 생성해주는 것 → merge의 기본 동작방식

### fast-forward merge

![git_fast_forward_merge](/Images/git_fast_forward_merge.png)

가끔은 새로운 브랜치에만 commit 이 있고 **기준이 되는 브랜치에는 신규 commit 이 없는 경우**, merge하면 "fast-forward merge 되었다" 라고 함.
이는 딱히 합칠 것이 없어 신규브랜치에게 "지금부터 너는 main 브랜치다" 라고 하는 것임. 물론 3-way merge 결과와 같음

<br/>

## git rebase & merge

![git_rebase](/Images/git_rebase.png)

브랜치의 시작점을 다른 commit으로 옮겨주는 것
rebase로 신규브랜치의 시작점을 main 브랜치 최근 commit으로 옮긴 다음, fast-forward merge하면 됨

```shell
git switch {새로운 브랜치}
git rebase main

git switch main
git merge {새로운 브랜치}
```

<br/>

## git squash & merge

![git_squash](/Images/git_squash.png)

작업 폴더에서 staging area로 옮겨주면서 commit할 파일들 staging 하기

```shell
git switch main
git merge --squash {branch명}
git commit -m '메세지'
```
