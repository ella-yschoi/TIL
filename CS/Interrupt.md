# 인터럽트(Interrupt)

<br/>

## 인터럽트란?

- 컴퓨터 시스템에서 발생하는 **하드웨어나 소프트웨어 이벤트**
- 현재 실행 중인 프로그램의 흐름을 중단하고 **다른 이벤트나 작업에 대한 처리를 수행하는 메커니즘**
- 인터럽트는 **시스템의 응답성**과 **다중 작업**을 관리하기 위해 사용됨

<br/>

## 인터럽트가 발생하는 상황

### 하드웨어 인터럽트

- 외부 하드웨어 장치(e.g. 키보드, 마우스, 타이머 등)가 주목할 만한 이벤트를 생성 시 발생
- 이를 통해 시스템은 해당 장치와 상호작용하거나 필요한 작업 수행 가능

### 소프트웨어 인터럽트

- 프로그램 내부에서 명시적으로 호출되는 소프트웨어 인터럽트나 예외 상황(e.g. 0으로 나누기, 메모리 접근 오류 등)으로 인해 발생
- 이는 프로그램의 비정상적인 동작을 처리하거나 오류를 처리하는 데 사용됨

<br/>

## 정리하자면

- 인터럽트 처리는 운영체제 또는 시스템의 하드웨어에 의해 수행되며,
- 인터럽트가 발생하면 현재 실행 중인 작업은 중단되고, 해당 인터럽트에 대한 처리가 수행됨.
- 이후에는 이전의 작업을 계속하거나 다른 작업으로 전환할 수 있음
- 인터럽트는 시스템의 효율성, 응답성 및 안정성을 유지하기 위한 중요한 개념으로, 다양한 운영체제 및 컴퓨터 아키텍처에서 지원하고 사용됨