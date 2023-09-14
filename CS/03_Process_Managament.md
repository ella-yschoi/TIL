# 03. 프로세스 관리

> Reference: [이화여자대학교 운영체제 강의 - 반효경](http://www.kocw.net/home/cview.do?cid=4b9cd4c7178db077)

<br/>

## 프로그램의 실행 (Memory load)

![memory_load](/Images/CS03_memory_load.png)

### 원리

- 프로그램은 실행 파일 형태로 저장되어 있다가
- 실행하면 해당 프로그램이 memory에 올라가서 process가 됨
- 이때, 운영체제 Kernel은 이미 memory에 올라가 있음
- 프로그램이 실행될 때 해당 프로그램만의 자신만의 독자적인 Address Space가 → Virtual memory
- 만약 당장 필요한 부분은 물리적인 momory에 올라감
- momory에 올라가 있지 않은 부분은 Swap area로 들어감
- 이 중 일부는 파일 시스템의 파일 형태로 존재

### Address Translation

- Virtual Memory Address (논리적 주소)와 Physical Memory Address (물리적 주소) 간 변환이 필요함

### Virtual Memory

#### stack

- 함수 안에 있는 지역 변수 데이터가 위치
- 함수 호출 및 return과 관련된 정보에 차곡차곡 쌓임

#### data

- 전역 변수 데이터가 위치
- 프로그램이 시작될 때부터 종료될 때까지 있는 값도 위치

#### code

- 실행 파일에 있던 code가 올라오는 것
- CPU에서 수행할 기계어가 위치 → 컴파일된 기계어 코드

### Kernel Address Space

- Kernel도 하나의 프로그램이기 때문에 함수 구조로 되어 있음
- 따라서 동일하게 stack, data, code로 구성되어 있음

<br/>

## Kernel Address 공간의 내용

![kernel_address](/Images/CS03_kernel_address.png)

### 구조

- 하나의 프로그램으로서 함수 구조로 되어 있음
- 프로세스 각각의 Adress Space에는 Code, Data, Stack으로 구성됨

### 운영체제의 Code

> 주로 운영체제가 하는 일이 Kernel Code 안에 들어가 있다고 보면 됨

- System call, Interrupt 처리 코드
- Interrupt가 들어왔을 때 무엇을 처리해야 하는지 들어가 있음
- 효율적인 자원 관리를 위한 코드
- 편리한 서비스 제공을 위한 코드

### 운영체제의 Data

- 현재 실행중인 하드웨어와 모든 프로세스들을 관리하기 위한 자료구조
- 이것을 PCB(Process Control Block) 라고 함

### 운영체제의 Stack

- 지금 누가 실행중인지를 알기 위해 process의 kernel stack은 각각 저장됨
- 각 프로세스마다 별도의 kernel을 두고 있음
- 즉, Kernel이 호출되기 전에 어떤 process에서 실행된 것인지에 따라 구분되어 저장되기 때문
- Kernel의 스택이기 때문에 Kernel 함수와 관련됨

<br/>

## 사용자 프로그램이 사용하는 함수

![function](/Images/CS03_function.png)

### 사용자 정의 함수

> 해당 process address space 내에 위치

- 내가 직접 만든 함수, 자신의 프로그램에서 정의한 함수
- program counter 값만 바꾸어 다른 위치의 기계어를 실행하면 됨
- 자신의 프로그램 안에 포함되어 있음

### 라이브러리 함수

> 해당 process address space 내에 위치

- 자신의 프로그램에서 정의하지 않고, 가져다 쓴 함수
- 내가 만든 함수는 아니고 프로그램 안에 집어 넣는 것
- 사용자 정의 함수와 마찬가지로, 자신의 프로그램 안에 포함되어 있음
- 이때는 내 프로그램 안에서 program counter 값만 바꾸어서 다른 위치의 기계어를 실행하는 원리

### 커널 함수

> kernel address space 내에 위치

- 운영체제 프로그램의 함수
- 프로그램 안에 들어가는게 아니라 커널 안에 들어가는 함수
- 실행되다가 디스크에서 파일을 읽어온다든지 하면 I/O는 내가 직접 할 수 있는게 아니기 때문에 사용자 정의/라이브러리 함수가 아닌 커널 함수 실행(system call)해야 함
- virtual memory의 주소 공간을 가로질러 다른 program 의 영역으로 바뀌는 것이기에  CPU 제어권을 OS에 넘긴 후 실행함

<br/>

## 프로그램의 실행

![program_execution](/Images/CS03_program_execution.png)

### User Defined Call & Library Function Call

- user mode (mode bit: 1)
- 내 주소 공간에 있는 code가 user mode로 실행됨

### System Call

- kernel mode (mode bit: 0)
- CPU 제어권이 운영체제에게 넘어가므로 Kernel mode에서 운영체제의 주소공간에 있는 코드가 실행됨

<br/>

## 프로세스의 개념

![process](/Images/CS03_process.png)

### 프로세스란?

- 실행중인 프로그램을 뜻함
- “*Process is a program in execution”*

### 프로세스의 문맥 (context)

#### 문맥이란

- 프로세스의 현재 시점의 상태를 나타내는 것
- 시간에 따라 바뀌는 개념

#### CPU 수행 상태를 나타내는 hardware context

> CPU에서 어디까지 수행했는가?

- program counter 값 → 현재 어디를 실행하고 있는가
- 각종 register 값 → → Register에 어떤 값을 넣고 있었는가

#### Process의 주소 공간

> 자신의 메모리 공간에 무엇을 가지고 있는가?

- code, data, stack

### Process 관련 Kernel 자료 구조

#### PCB(Process Control Block)

- CPU, memory 등을 얼마나 썼는지에 대한 정보를 갖고 있는 자료구조
- PCB를 봐야 context를 알 수 있기 때문에 프로세스를 관리하기 위한 자료구조라 할 수 있음

#### Kernel Stack

- process마다 다른 kernel stack을 가짐

<br/>

## 프로세스의 상태

> 프로세스는 상태(state)가 변경되며 수행된다

![process_state](/Images/CS03_process_state.png)

### Running

- CPU를 잡고 instruction을 수행중인 상태
- CPU가 하나밖에 없기 때문에 CPU에서 기계어를 실행하는 프로세스는 매순간 하나 → Running 상태에 있다고 함

### Ready

- CPU를 기다리는 상태(메모리 등 다른 조건을 모두 만족하고)

### Blocked(wait, sleep)

- 오래 걸리는 작업 때문에 CPU를 주어도 당장 instruction을 수행할 수 없는 상태
- process 자신이 요청한 event(e.g. I/O)가 즉시 만족되지 않아, 이를 기다리는 상태
- Inturrupt 되면 진행중이던 event가 완료 되었다는 의미이므로 Ready 상태로 바꿔줌
- e.g. Disc에서 file을 읽어와야 하는 경우

### New

- 프로세스가 생성’중’인 상태

### Terminated

- 수행(execution)이 끝난 상태

### 예시

- 키보드 입력을 기다리는 프로그램에서는 blocked 상태 → 키보드 입력 들어옴 → ready 상태로 바꾸고 → 키보드 입력된 내용을 메모리에 copy 해서 CPU 얻을 수 있게 해줌(CPU 제어권이 운영체제에게 넘어감)

<br/>

## 프로세스의 상태도

![process_state_picture](/Images/CS03_process_state_picture.png)

### new

- 생성 **중**인 상태
- 시작 전이면 프로세스가 아님

### ready

- CPU만 할당되면 바로 실행이 가능한 상태 즉, 온전히 프로세스가 된 상태
- CPU가 필요한 부분은 memory에 올라가 있어야 함

### running

- CPU scheduler가 dispatch(CPU를 넘겨주면)하면 running 상태가 됨
- running 상태가 끝나는 경우
  - Timer interrupt: 할당 시간 만료로 ready queue의 제일 뒤로 가 줄을 서야하는 상황
  - I/O or event wait: 오래 걸리는 작업 때문에 blocked 상태로 들어가는 경우
  - Exit: 종료되는 경우

### waiting(blocked)

- 오래 걸리는 작업이 끝나면 (보통 interrupt가 걸림) 해당 process의 상태를 ready로 바꿔서 다시 CPU가 해당 process를 실행할 준비를 시켜둠

### terminated

- 종료 **중**인 상태
- 이미 종료되었다면 프로세스가 아님

<br/>

## PCB

![pcb](/Images/CS03_pcb.png)

### 정의

- 운영체제가 각 process를 관리하기 위해 두는 자료구조
- process 당 유지하는 정보

### 구성 요소

- 운영체제가 관리상 사용하는 정보
  - Process State, Process ID
  - Scheduling Information, Priority (가장 높은 process에 CPU가 할당됨)
- CPU 수행 관련 hardware 값
  - Context Switching에 대비하여 저장해 놓는 값
  - Program Counter, Registers
- Memory 관련
  - code, data, stack의 위치 정보
- File 관련
  - Open file descriptors …

<br/>

## 문맥 교환 (Context Switching)

![context_switching](/Images/CS03_context_switching.png)

### 정의

- CPU를 한 process에서 다른 process로 넘겨주는 과정

### 필요한 이유

- CPU를 그냥 빼앗아 가는게 아니라, 바로 그 다음 지점을 실행할 수 있도록 현재 프로세스 문맥을 저장해야 함
- 즉, 만약 CPU가 process A에서 process B로 넘어가게 하려면, 현재 기계어의 어디 실행중인지 등 정보를 CPU 뺏기 전에 process A의 PCB에 저장 후, CPU를 넘겨줌

### 동작 과정

> CPU가 다른 프로세스에게 넘어갈 때 운영체제는 아래의 동작을 수행함

- CPU를 내어주는 프로세스의 상태를 해당 프로세스 PCB에 저장
- CPU를 새롭게 얻는 프로세스의 상태를 PCB에서 읽어옴

<br/>

## Context Switch 구분하기

![context_switch_difference](/Images/CS03_context_switch_difference.png)

### context switch인 것

- 사용자 process A ↔ 사용자 process B

### context switch가 아닌것

- 사용자 process A → 운영체제 → (다시) 사용자 process A

### context switch 여부와 overhead 관계

- user mode에서 kernel mode로 가는건 context switch보다 상대적으로 overhead가 적은 작업
- context switch 없이 CPU 수행 정보 등 context의 일부를 PCB에 save 해야 하지만
- context switch 하는 경우, 그 부담이 훨씬 큼 (캐시 메모리 flush 할 때 overhead가 매우 큼)

<br/>

## Process를 스케줄링 하기 위한 Queue

> 프로세스들은 각 queue를 오가며 수행됨

### job queue

- 현재 시스템 내에 있는 모든 프로세스의 집합

### ready queue

- 그 중 CPU를 당장 얻어야 하는 집합
- 현재 메모리 내에 있으면서, CPU를 잡아 실행되기를 기다리는 프로세스의 집합

### device queue

- 오래 걸리는 작업
- I/O device의 처리를 기다리는 프로세스의 집합

<br/>

## 실제 자료구조 형태

![data_structure](/Images/CS03_data_structure.png)

<br/>

## Process 스케줄링 Queue의 모습

![process_scheduling_queue](/Images/CS03_process_scheduling_queue.png)

- process가 처음에 실행되면 ready queue
- 본인 차례가 되면 CPU를 얻고 쓰다가 언젠가는 종료
- 쓰다가 오래 기다리는 작업을 요청하면 → I/O queue 가서 줄서고
- 끝나면 다시 ready queue에서 CPU 얻을 권한 생기고
- CPU 계속 쓰고 싶은데 timer interrupt 끝나면
- 다시 ready queue로 감
