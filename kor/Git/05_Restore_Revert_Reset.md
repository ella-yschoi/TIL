# git restore, revert, reset

<br/>

## git restore : 파일 하나를 되돌리기

최근 commit된 상태로 현재 파일의 수정내역을 되돌리기

```shell
git restore 파일명
```

입력한 파일을 특정 커밋아이디 시점으로 복구하기

```shell
git restore --source 커밋아이디 파일명
```

특정 파일을 staging 취소

```shell
git restore --staged 파일명
```

<br/>

## git revert : commit을 되돌리기

과거의 커밋 내역을 취소하고자 한다면, commit 하나를 취소한 commit을 추가 생성. 즉, 특정 커밋에서 있던 일을 지워버릴 수 있는 명령어임.

```shell
git revert 커밋아이디
```

![git_revert](/Images/git_revert.png)

- vim 에디터가 뜬다면 commit message 수정 후 닫기
- revert 시, 동시에 여러개의 commit id 입력 가능
- 최근 했던 commit 1개만 revert : git revert HEAD 입력
- merge 명령으로 인해 새로 만들어진 commit도 revert 가능

<br/>

## git reset : 전부 되돌리고 싶다면

특정 commit 때로 아예 모든 것을 되돌릴 수 있음 (작업 폴더 내 파일 포함)

```shell
git reset --hard 커밋아이디
```

![git_reset](/Images/git_reset.png)

- 다만, **협업 프로젝트 시에는 사용을 매우 주의**해야 함
- untracked 파일들은 (git add 안 해놓은 파일들은) 사라지지 않고 유지됨
- git clean 명령어는 untracked 파일들도 다 지울 수 있음 (더 위험..)
- reset하면서 파일을 아예 지워버리는게 아니라, (staging을 취소하면서) 검토하고 다시 commit 하고 싶다면 `--hard`가 아닌, `--soft`나 `--mixed`을 사용
- 물론 `git reset` 입력 시, `--mixed` 옵션이 기본으로 작동되며, 인덱스(Staging Area)만 초기화됨.
