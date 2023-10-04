# Blocking vs. Non-blocking

## Blocking과 Non-blocking이란?

- 프로그래밍 및 컴퓨터 시스템에서 **작업의 실행**과 관련된 두 가지 주요 접근 방식
- Blocking과 Non-blocking의 주요 차이점은 **작업의 의존성**과 **동시성 처리**에 있음

## Blocking

- **한 작업이 실행 중일 때 다른 작업은 해당 작업이 끝날 때까지 대기해야 하는 상황**을 의미
- 이는 작업이 완료될 때까지 **시스템의 자원과 제어권을 독점**하는 것을 의미한다.
- 이로 인해 다른 작업들은 블로킹된 작업이 완료될 때까지 대기해야 하므로 전체 시스템 성능에 영향을 줄 수 있음

## Non-blocking

- 한 작업이 실행 중일 때 **다른 작업들도 병렬로 실행**될 수 있으며, 작업 간에 **상호 간섭이 없는 상태**를 의미
- Non-blocking 방식에서는 **작업 간의 의존성이 줄어**들어 **전체 시스템 성능이 향상**되고, 하나의 작업이 실패하더라도 다른 작업들은 계속 진행할 수 있음