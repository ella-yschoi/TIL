# Branch Strategy

<br/>

## 브랜치 종류

1. main
2. develop
3. feature/xxx
4. release/xxx
5. hotfix/xxx

<br/>

## 전체적인 브랜치 전략 흐름

1. 어떠한 제품의 요구(Theme) 발생 시 하나의 repository가 생성되며 그와 동시에 main branch가 생성
2. main branch가 생성되면 바로 개발을 위한 develop branch를 생성하고 이를 default branch로 설정
3. Feature branches는 develop branch로부터 생성되며 하나의 기능(Story)을 작성할 때 마다 발생
4. 하나의 feature branch가 개발이 완료되면 develop branch(Epic)에 병합
5. Story가 모여 한 Epic을 이루게되면 release branch가 생성
6. Release branch가 완료되면 main branch와 develop branch 모두에 병합
7. 만약 main branch에서 문제가 감지되면 hotfix branch는 main branch로 부터 생성
8. Hotfix branch가 완료되면 main branch와 develop branch 모두에 병합

<br/>

## 브랜치별 규칙

### main

- main 브랜치는 공식 릴리즈 기록을 저장
- release 브랜치로부터의 PR 수락은 해당 프로젝트의 담당자가 수행
- 요청온 release 브랜치의 문제가 없음을 확실히 확인했음을 의미

### develop

- develop은 분기 기능(branch) 개발의 통합 지점 역할
- develop으로의 merge는 통합되는 branch의 리뷰 및 테스트가 완료되었음을 의미

### feature/xxx

- xxx의 의미는 작성되는 기능을 의미 e.g. 인증 기능 개발시 : feature/auth
- 하나의 기능은 새로운 브랜치를 생성하여 개발되어야 하며, 그 이름(naming)은 해당 브랜치가 어떤 기능을 수행하는지 명확히 해야함
- 해당 branch의 MR은 sprint 퇴고 전 마스터에게 담당자가 요청하며, 마스터가 해당 기능의 문제 없음을 동의 및 수락의 의미로 승인
- 해당 브랜치 수정 및 추가시 마이너버전이 업그레이드
- 아주 가끔의 경우(중요도에 따라), 미들버전이 업그레이드

### release/xxx

- xxx의 의미는 출시 버전의 규칙에 따른 숫자의 나열 e.g. 1.2.3
- develop 브랜치가 출시를 위한 충분한 기능 개발이 완료되었거나 출시 일정이 다가오고 있다면 생성
- 만들어진 release 브랜치에서 출시를 위한 준비 완료시 main으로의 PR생성
- 숫자는 버전명이며, 아래과 같은 규칙으로 ‘.’ 으로 구분하여 나열
  - Major version : Theme의 update
  - Middle version : Epic단위의 update or Epic으로 다룰수도 있을 큰 수준의 Story update
  - Miner version : Story단위의 update 및 패치

### hotfix/xxx

- xxx의 의미는 생성된 이슈의 의미
- hotfix 브랜치 생성의 의미는 출시한 제품의 중대한 버그가 발생했음을 의미
- 릴리즈를 빠르게 패치하는 데 사용

<br/>

## 브랜치별 명령어

### Develop Branch

```shell
git branch develop
git push -u origin develop
```

- 초기 생성시, main 브랜치에서 develop 브랜치를 생성하고 서버로 푸시
- Epic단위로 main에 merge

### Feature Branches

```shell
git checkout develop
git checkout -b feature/branch
```

- 각각의 새로운 기능(Story)은 새로운 브랜치를 생성하여 개발해야 함
- 즉, 어떤 단위의 기능을 구현할 때 develop 브랜치에서 해당브랜치를 생성하여 개발
- 브랜치 생성시, 네이밍은 해당 브랜치가 어떤 기능을 수행하는지 명확히 해야함

```shell
git checkout develop
git merge feature/branch
git branch -d feature/branch
```

- 일반적으로 feature 브랜치는 가장 최신 develop 브랜치에서 생성
- Task단위로 commit을 진행
- Story 완성시 백업 / 협업 / 코드리뷰를 위해 서버(remote)로 푸시
- 코드리뷰 요청시, 리뷰 수행자는 해당 브랜치를 가져와서 확인하고 리뷰
- 한 가지 기능에 대해 개발이 완료되면, 다시 develop 브랜치로 병합하고, feature 브랜치는 삭제
- **feature 브랜치는 절대로 main 브랜치와 직접적으로 상호작용하지 않음**

### Release Branches

```shell
git checkout develop
git checkout -b release/0.1.0
```

- release 브랜치를 만드는 것은 출시 시점에 맞춰 develop 브랜치로부터 생성
- develop 브랜치가 출시를 위한 충분한 기능 개발이 완료되었다면
- 또는 출시 일정이 다가오고 있다면 만들어진 release 브랜치에서 출시를 위한 준비를 시작
- release 브랜치에 새로운 기능 개발은 추가할 수 없음
- 단지 버그 수정, 설명서 생성 및 기타 출시 준비 작업만 수행

```shell
git checkout main
git merge release/0.1.0
git checkout develop
git merge release/0.1.0
git branch -d release/0/1/0
```

- 출시 전용 브랜치를 사용하여 출시 준비를 하는 한편, 다른 팀은 다음 출시 기능 개발을 진행 가능
- 출시 준비가 완료되면, release 브랜치를 main 브랜치와 develop 브랜치에 병합하고 release 브랜치는 삭제
- release 브랜치를 main 브랜치에 병합하고 버전 정보를 태그

### Hotfix Branches

```shell
git checkout main
git checkout -b hotfix/branch
```

- hotfix 브랜치는 릴리즈를 빠르게 패치하는 데 사용
- hotfix 브랜치는 main 브랜치에서 생성

```shell
git checkout main
git merge hotfix/branch
git checkout develop
git merge hotfix/branch
git branch -D hotfix/branch
```

- 수정 사항이 완료되면, main 브랜치와 develop 브랜치 (또는 현재의 release 브랜치)에 병합하고 main 브랜치에 업데이트된 버전을 태그
- 수정 사항이 완료되면, release 브랜치와 같이 hotfix 브랜치는 main 브랜치와 develop 브랜치 모두에 병합하고 hotfix 브랜치는 삭제
