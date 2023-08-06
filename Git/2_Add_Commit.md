# git add, commit

## 작업 폴더에서 git 이용하기

- 새로운 Git 저장소 (repository)를 생성하는 명령어를 입력하면, 현재 디렉토리를 기준으로 Git 저장소가 생성된다.

  ```shell
  git init
  ```

<br/>

## add하고 commit해서 버전 만들기

- 작업 폴더에서 staging area로 옮겨주면서 commit할 파일들 staging 하기

  ```shell
  git add 파일이름
  ```

- 여러 개의 파일 staging 하기

  ```shell
  git add 파일이름1 파일이름2
  ```

- 모든 파일 staging 하기

  ```shell
  git add .
  ```

- 현재 변경된 파일, staging된 파일들을 알고 싶다면 아래 명령어 입력하기

  ```shell
  git status
  ```

- staging area에서 파일을 제외하고 싶다면 아래 명령어 입력하기

  ```shell
  git restore --staged 파일이름
  ```

- staging area에서 repository로 옮겨주기

  ```shell
  git commit -m '커밋 메시지 작성'
  ```

- commit한 기록을 한 눈에 파악하고 싶다면 아래 명령어 입력하기

  ```shell
  # 텍스트로 보여줌
  # 입력 후 Vim 에디터가 켜지면 j, k 키로 위아래 스크롤 가능, q 키로 종료 가능
  git log
  ```

  ```shell
  # 그래프로 보여줌
  # 입력 후 Vim 에디터가 켜지면 j, k 키로 위아래 스크롤 가능, q 키로 종료 가능
  git log --graph
  ```
