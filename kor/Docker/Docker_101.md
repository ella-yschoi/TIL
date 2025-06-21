# Docker 101

> References: [Docker Official Docs](https://docs.docker.com/get-started/overview/)

## Docker란?

- 애플리케이션 구축, 구현, 테스트를 위해 **격리된 가상화 환경을 생성하는 서비스형 플랫폼**
- Docker 사용 시, 애플리케이션을 인프라에서 분리해 소프트웨어를 빠르게 실행 가능


<br/>

## Docker의 구조

![docker_structure.png](/images/docker_structure.png)

- Docker는 클라이언트-서버 아키텍처를 사용함.
- **Docker 클라이언트**는 Docker Container를 빌드, 실행 및 배포하는 무거운 작업을 수행하는 **Docker Deamone과 통신**함.
- Linux Kernel 기능을 사용해 운영체제 위에 Container를 만들고, Docker 자체에는 서비스의 Container를 관리하는 Deamone으로 실행됨.
- 실제 Container를 생성하고, Images를 **관리하는 주체는 Docker 서버**이며, Docker 엔진 프로세스에서 동작함.
- Docker 엔진은 외부에서 API 입력을 받아 Docker 엔진의 기능을 수행함.
- Docker 프로세스가 실행되어 **서버로서 입력을 받을 준비가 된 상태**를 Docker Deamone이라고 함
- `docker`로 시작하는 명령어를 입력하면 Docker 클라이언트를 사용하는 것임.
- Docker 클라이언트는 입력된 명령어를 로컬에 존재하는 Docker Deamone에게 API로서 전달함
- 이때 Docker 클라이언트는 /var/run/docker.sock에 위치한 소켓을 통해 Docker Deamone의 API를 호출

<br/>

## Container란?

- 실제 화물 선박에서 사용하는 Container처럼 애플리케이션을 **일관성 있게 표준화된 형태로 전달하는 기능을 제공**
- 느슨하게 격리된 환경에서 애플리케이션을 패키징하고, 실행할 수 있는 기능 제공
- 격리 및 보안을 통해 지정된 호스트에서 여러 Container를 동시에 실행 가능
- 가볍고 애플리케이션 실행에 필요한 모든 것을 포함하므로 호스트에 설치된 항목에 의존할 필요 없음. 즉, 모든 사람이 동일한 방식으로 작동하는 동일한 Container를 갖게 되는 것
- 따라서 Docker는 **개발자가 애플리케이션과 서비스를 제공하는 로컬 Container를 사용하여 표준화된 환경에서 작업할 수 있도록 함**.
- Container는 CI/CD 워크플로우에 적합하기도 함

<br/>

## Daemon이란?

- Docker API 요청을 수신하고 Images, Container, 네트워크 및 볼륨과 같은 Docker 객체를 관리함.
- Daemon은 다른 Daemon과 통신하여 Docker 서비스를 관리할 수도 있음.

<br/>

## Image이란?

- Appliaction 패키징 및 전송을 위해 사용함.
- Appliaction 실행에 필요한 독립적인 환경을 포함하며, **런타임 환경을 위한 일종의 템플릿**이라고 볼 수 있음.
- 소스 코드, 라이브러리, 종속성, 도구 및 응용 프로그램을 실행하는데 필요한 기타 파일을 포함하는 불변 파일임.
- 이미지는 읽기 전용이므로 스냅샷 이라고도 하며, 특정 시점의 application과 가상 환경을 나타냄.
- 이러한 일관성은 docker의 큰 특징 중 하나로, 개발자가 안정적이고 균일한 환경에서 소프트웨어를 테스트하고 실험할 수 있도록 함.