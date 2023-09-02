# Install Git

<br/>

## 맥에서 brew 설치하기

1. [Git 홈페이지](https://git-scm.com/) 접속 후, [Download for Mac] 클릭해 다운로드 받기
2. 맥 내에서 terminal 열기
3. [Homebrew 홈페이지](https://brew.sh/) 접속 후, 아래 명령어를 terminal에 입력하기

   ```shell
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

4. terminal에 맥 로그인 시 입력하는 password 입력하기
5. 설치 완료 후, 도움말 명령어를 입력해 설치가 잘 되었는지 확인하기

   ```shell
   brew help
   ```

6. 만약 `zsh: command not found: brew` 와 같은 에러가 난다면, M1 Mac을 사용하고 있기 때문에 발생한 것이니 아래 명령어 입력하기

   ```shell
   eval $(/opt/homebrew/bin/brew shellenv)
   ```

<br/>

## 맥에서 Git 설치하기

1. 터미널에 git 설치 명령어 입력하기

   ```shell
   brew install git
   ```

2. 설치 후 버전 확인하는 명령어를 입력했을 때 버전 정보가 잘 나온다면 정상적으로 설치 완료!

   ```shell
   git --version
   ```

3. 추가로, 기본 브랜치 이름을 `master`에서 `main`으로 변경하고 싶다면 아래 명령어를 입력하기

   ```shell
   git config --global init.defaultBranch main
   ```

4. 기기에서 git을 처음 사용한다면 아래 명령어를 차례대로 입력하기

   ```shell
   git config --global user.email "ella@gmail.com"
   git config --global user.name "Ella"
   ```
