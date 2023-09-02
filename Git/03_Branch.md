# git branch

<br/>

## branch 명령어

### branch 확인

  ```shell
  # * 표시로 현재 작업중인 브랜치 확인 가능
  git branch
  ```

### branch 생성 후 해당 브랜치로 전환

  ```shell
  git branch {생성하려는 branch명}
  ```

  ```shell
  git checkout -b {생성하려는 branch명}
  ```

  ```shell
  git switch -c {생성하려는 branch명}
  ```

### branch 이동

  ```shell
  git checkout {이동하려는 branch명}
  ```

  ```shell
  git switch {이동하려는 branch명}
  ```

### branch 병합

  ```shell
    # merge를 위해 main 브랜치로 전환
    git switch main

    # main 브랜치로 feat/todo 브랜치를 병합
    git merge feat/todo
  ```

다만, 실제 프로젝트 개발 시에는 브랜치를 로컬에서 합치기보다는 GitHub의 pull request 기능을 이용하여 변경 내역을 충분히 확인하고 난 다음에 머지하는 경우가 더 많기 때문에, 로컬에서 머지하지 않고 feature 브랜치를 push하여 PR를 요청하는 것을 권장
  
```shell
  # GitHub repository로 push
  git push origin feat/todo
  # GitHub에서 Pull Request 및 merge
```

### branch 삭제

  ```shell
  # merge한 브랜치 삭제
  git branch -d {삭제하려는 branch명}

  # merge하지 않은 브랜치 삭제
  git branch -D {삭제하려는 branch명}
  ```

<br/>

## branch 관련 에러

- 브랜치를 삭제하려고 할 때 다음과 같은 에러가 나올 수 있다. 이는 브랜치에서 수정한 내용을 **merge 하지 않아서 나오는 에러**이다. 딱히 수정 내용이 중요하지 않다면 `git branch -D`를 입력해강제로 브랜치를 삭제 하면 된다.

  ```shell
  error: The branch 'branchname'isnot fully merged.
  If you are sure you want todelete it, run 'git branch -D branchname'.
  ```

- 다만 위 강제 삭제는 어디까지나 로컬상의 브랜치를 삭제한 것이므로 리모트 서버 상의 브랜치도 삭제를 해야 한다.