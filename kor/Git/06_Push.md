# git push

<br/>

## 1. VScode에서 Github Repository로 올리기

### (1) Github에서 새로운 Repository 생성하기

- 본인 Github 프로필 화면 좌측 상단의 Repositories 클릭 → 우측 상단의 [New] 버튼 클릭
- Owner, Repository name, Description, README 여부 등을 설정 후 [Create Repository] 클릭

### (2) VScode를 열어 새로운 파일을 생성하기

- 폴더(Github에 올릴 Repository)를 만들기
- 해당 폴더 안에 새로운 파일을 생성하기

### (3) git 초기화

```shell
git init
```

- 혹은 VScode 좌측 브랜치 모양의 아이콘인 Source Control 창에서 [Initialize Repository] 버튼 클릭해 초기화
- 로컬에서 Repository를 생성하면서 초기화하는 것
- 이제 이 폴더에 있는 파일들을 git 명령어들을 이용해 관리하겠다는 의미

### (4) push할 목록에 올려두기

```shell
git add
git commit
```

### (5) Github에서 만든 Repository에 올리기

```shell
git push -u Repository 주소 branch명

# 예시
git push -u https://github.com/ella-yschoi/TIL.git main
```

- main 브랜치를 Repository에 올린다는 의미
- github 로그인 하라고 하면 로그인하면 됨
- `-u` 옵션은 방금 입력한 주소를 기억해 두라는 뜻이며, 다음부터는 주소를 길게 입력하지 않아도 git push만 입력해도 됨.

<br/>

## 2. Repository 주소를 길게 입력하는 것이 귀찮다면

### (1) Repository 주소를 변수로 저장하기

```shell
# Repository 주소를 변수로 저장
git remote add origin Repository 주소 branch명

# 예시
git remote add origin https://github.com/ella-yschoi/TIL.git main
```

```shell
# Repository 주소를 변수로 저장한 이후 push
git push origin branch명

# 예시
git push origin main
```

### (2) 변수 목록을 살펴보고 싶다면

```shell
git remote -v
```
