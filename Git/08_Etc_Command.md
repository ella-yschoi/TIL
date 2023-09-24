# Etc. Command

<br/>

## 도움말 보기

help 명령어로 각 명령어 및 옵션의 기능에 대해 살펴볼 수 있음

```shell
# Git에서 제공하는 모든 명령어 보기
$ git help -all
```

```shell
# 특정 command에서 사용할 수 있는 모든 옵션 보기
$ git [command] -help
```

<br/>

## 세팅 및 초기화

Repository를 초기화하거나 존재하는 Repository를 clone

```shell
# 현재 directory를 기준으로 Git 저장소가 생성
$ git init
```

```shell
# URL을 통해 remote Repository를 local Repository에 복제
$ git clone [url]
```

<br/>

## Stage & Commit

stage 영역을 이용하여 commit할 수 있음

```shell
# 다음 commit을 위해 현재 directory에서 수정된 파일을 확인할 수 있음
$ git status
```

```shell
# 다음 commit을 위해 파일을 추가 (stage)
$ git add [file]
```

```shell
# 추가한 파일을 unstaging: 변경 사항은 유지됨
$ git reset [file]
```

```shell
# stage되지 않은 변경 사항을 보여줌
$ git diff
```

```shell
# stage했지만 commit하지 않은 변경 사항을 보여줌
$ git diff --staged
```

```shell
# stage된 콘텐츠를 메시지와 함께 commit (snapshot 생성)
$ git commit -m “[descriptive message]”
```

<br/>

## 비교 및 검사

로그 및 변경 사항을 검사할 수 있음

```shell
# 브랜치B에 없는 브랜치A의 모든 commit 히스토리를 보여줌
$ git log branchB..branchA
```

```shell
# 해당 파일의 변경 사항이 담긴 모든 commit을 표시 (파일 이름 변경도 표시)
$ git log --follow [file]
```

```shell
# 브랜치A에 있지만 브랜치B에 없는 것의 변경 내용(diff)을 표시 (branch간 상태 비교)
$ git diff branchB...branchA
```

<br/>

## 공유 및 업데이트

특정 Repository의 업데이트 사항을 검색하여 local Repository를 업데이트 할 수 있음

```shell
# url을 통해 특정 remote Repository를 별칭으로 추가
$ git remote add [alias] [url]
```

```shell
# 별칭으로 추가한 remote Repository에 있는 모든 브랜치 및 데이터를 local로 가져옴
$ git fetch [alias]
```

```shell
# remote 브랜치를 현재 작업중인 브랜치와 병합하여 최신 상태로 만들 수 있음
$ git merge [alias]/[branch]
```

```shell
# local 브랜치의 commit을 remote 브랜치로 전송
$ git push [alias] [branch]
```

```shell
# remote Repository의 정보를 가져와 자동으로 local 브랜치에 병합
$ git pull
```

<br/>

## 히스토리 수정

브랜치 또는 commit을 수정하거나 commit 히스토리를 지울 수 있음

```shell
# 특정 브랜치의 분기 이후 commit을 현재 작업중인 브랜치에 반영
$ git rebase [branch]
```

```shell
# 득정 commit 전으로 돌아가며 stage된 변경 사항을 모두 지움
$ git reset --hard [commitish]
```

<br/>

## 임시 저장

브랜치를 전환하기 위해 변경되었거나 추적 중인 파일을 임시로 저장할 수 있음

```shell
# 수정하거나 stage된 변경사항을 스택에 임시 저장하고 현재 작업 내역에서 지움
$ git stash
```

```shell
# 스택에 임시 저장된 변경사항의 목록을 보여줌
$ git stash list
```

```shell
# 스택에 임시 저장된 변경사항을 다시 현재 작업 내역에 적용
$ git stash apply
```

```shell
# 스택에 임시 저장된 변경사항을 다시 현재 작업 내역에 적용하고 스택에서 삭제
$ git stash pop
```

```shell
# 스택에 임시 저장된 변경사항을 삭제
$ git stash drop
```
