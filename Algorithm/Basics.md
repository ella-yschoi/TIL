## **자료구조 Basics**
### 1. Stack
- Stack의 구조
  - 입력과 출력이 하나의 방향, 즉 스택의 최상단에서만 이루어지는 제한적 접근
  - 이러한 Stack의 자료구조 정책: LIFO(Last In First Out) 혹은 FILO(First In Last Out)
  - Stack에 데이터를 넣는 것: push, 꺼내는 것: pop
- Stack의 특징
  - LIFO(Last In First Out): 후입선출
  - 하나의 입출력 방향을 가짐
  - 데이터는 하나씩 넣고 뺄 수 있음
- Stack 실사용 예제
  - 브라우저 뒤로가기, 앞으로 가기 기능 구현

<br/>

### 2. Queue
- Queue의 구조
  - 먼저 들어간 데이터가 먼저 나오는 FIFO(First In First Out) 혹은 LILO(Last In Last Out)
  - 입력과 출력의 방향이 각각 고정되어 있으며 데이터 입력시 큐의 끝에서, 데이터 출력시 큐의 맨 앞에서 진행
- Queue의 특징
  - FIFO(First In First Out): 선입선출
  - 두 개의 입출력 방향
  - 데이터는 하나씩 넣고 뺄 수 있음
- Queue의 실사용 예제
  - 컴퓨터와 연결된 프린터에서 여러 문서를 순서대로 인쇄
  - 속도와 시간 차이를 극복하기 위해 임시 기억 장치의 자료구조로 Queue를 사용(=버퍼)