---
layout: post
categories:
  - os
title: "[Lecture - OS] 04. Processes and Threads"
date: 2024-05-03 17:35:00 +09:00
tags:
---
# \[Lecture - OS] Processes and Threads

## Agenda

1. Process Concepts
2. Process Scheduling
3. Context Switching
4. Process Creation and Termination
5. Multithreading

## 1. Process Concepts

### Process Concepts

#### Why use Process?

- System 내부에서 여러 일이 일어날 때, 깔끔하게 구분될 필요가 있다.
- Decomposition
	- 어려운 문제를 여러 간단한 문제로 각각 해결한다.

#### What is Process?

- 정의
	- Program in execution or
	- Execution stream in the context of a particular process state
	- 간단히 실행 중인 프로그램이다.
- Process State
	- Process에 영향을 주고 받을 수 있는 모든 것.
	- code, data values, open files, etc.
- Execution Stream
	- Process State 내부에서 동작하는 instruction의 순서.
	- Process의 특징을 간략하게 표현할 수 있다.
	- 한 Process에서 한 번에 하나의 일만 일어날 수 있다.
	- 수행의 주체로, scheduling의 대상이 된다.

#### Process State or Context

- Context의 세 가지 types
	- Memory Context
		- code/data/stack segment, heap
	- Hardware Context (Register 내부 값)
		- CPU/I/O registers
	- System Context (OS가 Process를 관리하기 위한 것들)
		- process table(control block의 모음), open file table, page table
- Process의 개념 구현.

#### Multiprogramming vs. Multiprocessing

- Uniprogramming
	- 한 time에 하나의 process만 memory에 존재한다.
	- 과거 PC OS.
	- OS의 몇몇 부분을 간단히 하지만, 많은 것들을 어렵게 한다.
- Multiprogramming
	- Memory에 multiple process가 존재한다.
	- 대부분 system은 multiprogrammimg을 지원한다.
- Multiprocessing
	- 동시에 여러 process가 실행된다.
	- CPU가 복잡해진다.

#### Design-time Entity vs. Run-time Entity

- System design은 아래의 과정이다.
	- System requirements를 수용
	- Collection of tasks 생성
		- Decomposition하게 만듦
- Design-time Entity
	- Task
- Run-time Entity
	- Process
- Implementation
	- Design-time Entity를 Run-time Entity로 옮기기.

#### Large SW Develop Sequence

![sw_develop_seq](public/img/sw_develop_seq.png)

### Process Control Block

#### With Multiprocessing, OS must keep track of Processes

- PCB(Process Control Block)가 저장하는 요소
	- Execution state (save registers, etc.)
	- Scheduling information (priority)
	- Accounting and other misc. information (open files)
- System-wide table of PCB
	- Process table
- Unix
	- PCB의 크기는 고정돼있다.

### State Transition

#### Process를 수행함에 따라 state가 변한다.

- New
	- Process가 생성됨.
- Running
	- Instruction이 수행 중.
- Waiting
	- Process가 다른 event가 일어나길 기다림.
- Ready
	- Process가 CPU 할당을 기다림.
- Terminated
	- Process 수행이 끝남.

#### State Transition Diagram

![state_transition_diagram](/public/img/state_transition_diagram.png)

- Terminated
	- kill도 포함된다.
- Interrupt
	- Hardware interrupt
	- Async.
	- CPU protection
- Waiting for I/O or Event
	- Sync.
	- Software interrupt (system call)

#### State transitions and Scheduling queues

- Queue
	- Ready Queue
		- Main memory에 존재하는 하는 모든 process의 집합.
		- 실행을 ready or waiting
	- Device Queue
		- I/O device를 기다리는 모든 process의 집합.
- State transition
	- 여러 queue들을 이동하는 process

## 2. Process Scheduling

>Preemptive > Async. interrupt\
>
>Non-preemptive > Sync. interrupt


### Process Scheduling

#### Goal

- OS는 CPU를 공유하는 process 중 다음 실행할 것을 선택해야 한다.

#### Constraints

- Fair Scheduling
	- 모든 process는 실행 될 기회를 얻어야 한다.
- Protection
	- Process는 다른 process를 부술 수 없다.

### Scheduler Design Principle

#### Principle in designing system software

- Policy and Mechanism의 분리.
	- Scheduling Policy와 Dispatching Mechanism(Context Switching)은 분리돼있다.
- Two-level architecture

### Dispatcher

>Dispatcher는 Interrupt다!

#### Process를 작동하는 OS의 최심부

`loop forever`
`{`
	`run the process for a while`
	`stop it and save its state(Context save/store)`
	`load state of another process(Context restore)`
`}`

#### Challenges

1. Dispatcher가 어떻게 control을 되찾을 것인가?
	- CPU는 한 번에 하나만 수행할 수 있다.
	- 사용자 process가 동작하는 것은 dispatcher는 동작하지 않음을 의미한다.
2. 어떤 process를 다음에 실행할 것인가?
	- 실행할 수 있는 process를 효과적으로 정해야 한다.

### 1. Entering and Leaving the Kernel

#### Dispatcher가 control을 되찾는 과정.

- Non-preemptive
	- Process가 자발적으로 한다.
	- 가끔 process가 잘못 동작할 수 있다.
- Preemptive
	- 강제로 실행한다.
	- Timer hardware and Interrupts.

#### Kernel

- 오해
	- 사용자 process처럼 kernel은 thread of control을 보유한 능동적이고 독립적인 entity다.
	- Kernel은 사용자 process가 돌아가는 동안 계속 monitoring 한다.
- 진실
	- Kernel은 kernel function과 ISR로 이루어진 수동적 entity다.
	- Library와 비슷하다.
	- A collection of functions는 kernel space에서 돌아간다.

#### Kernel Space(Mode)

- 일반적인 사용자 app과 비교해 높은 system state를 가지고 있다.
	- 보호된 memory 공간
	- 모든 hardware에 접근 가능
- Elevated System State & Unrestriced Memory Access

#### User Space(Mode)

- Kernel과 비교해 제한된 system state를 가지고 있다.
	- 사용 가능한 machine의 subset.
	- Limited previlege
		- 특정 system funcs를 사용할 수 없다.
- Restricted System State & Restricted Memory Access

#### PWS(Process State Word)에 따라 execution mode가 나뉜다.

#### 즉, Dispatcher는 Kernel Function이다.

#### OS가 control을 얻는 방법

- Traps (Sync)
	- System call
	- Error
	- Page faults
- Interrupts (Async)

#### Process의 mode change

- syscall은 mode만 바뀐다.
	- context switching 일어나지 않는다!
	- PID는 유지된다.

#### System Call vs. Function Call

- 공통점
	- Control을 넘긴다.
	- Context를 유지한다.
- 차이점
	- Syscall은 mode change가 일어난다.
	- Syscall의 overhead가 더 크다! (expensive)

### Scheduling Policy

#### Dispatcher가 control을 얻고 다음을 일을 방법

- Process table 탐색
	- 시간이 오래 걸린다.
- Queue
	- Queue의 head를 선택한다.
- Priority
	- Queue에 priority 순서로 저장한다.
	- Priority에 따라 저장한다.

#### Priority

- OS가 결정한다.
	- Policy와 mechanism의 분리 때문에 dispatcher가 아닌 OS가 결정한다.

## 3. Context Switching

>Context는 여기서 collection of a process states를 의미한다.\
>Memory(code, data, stack, heap)는 Swapping에서 저장한다.\
>Interrupt는 context switching이 일어나지 않는다.\
>Blocking syscall에선 context switching이 일어난다!\
>Dispatcher가 process states를 save/restore 하는 mechanism

### Context Switching

#### 무조건 저장해야 하는 것

- 다음 Process가 영향을 줄  수 있는 것들
	- PC(Program Counter)
	- Processor Status Word (condition code, etc.)
	- General purpose Registers, Floating point Registers
- 고려 사항
	1. Memory를 저장하지 않음.
		- Dynamic memory는 관리하지 않음.
			- Memory는 전체 batch에 할당됨.
		- 과거 batch processing system(Multiprogrammed batch monitor)
		- Multithreaded process에서 context switching
	2. Memory를 모두 disk에 저장.(roll-in/roll-out swapping)
		- Process 실행 후 전체를 disk에 저장
			- 다른 program이 disk에서 자신의 memory를 load.
		- 초기 PC/PW: DOS
		- 효과적이나 너무 느리다.
	3. Memory의 일부분을 disk에 저장.
		- RAM과 disk 사이에서 process의 memory block을 이동.
			- Swap file/device
		- 복잡한 memory 관리 machanism
		- 대부분의 최신 OS에서 사용한다.

### Implementation

#### Machine dependent

- CPU register를 저장해야 하므로 의존적이다.

#### Tricky

- OS는 process의 state 변화 없이 state를 save하는 code를 실행해야 한다.

#### 특정 hardware의 도움이 필요하다.

- HW가 interrupt 지원 시 context switching이 쉽다!!

### Mechanism

#### Save

| StkPtr     | Properties                          |
| ---------- | ----------------------------------- |
|            | OS-PCB                              |
|            | HI-MEM                              |
| PSW        | INT call---CPU SP#1                 |
| SEG task   |                                     |
| OFF task   | INT call---                         |
| AX         | pusha---CPU SP#2                    |
| CX         |                                     |
| BX         |                                     |
| SP         | ->AX                                |
| BP         |                                     |
| SI         | pusha---                            |
| DI         |                                     |
| ES         | ->StkPtr,<br>push es 필요<br>CPU SP#3 |
| go to RunQ | LO-MEM                              |

#### Restore/Load

| StkPtr    | Properties                          |
| --------- | ----------------------------------- |
|           | OS-PCB                              |
|           | HI-MEM                              |
| PSW       | INT call---CPU SP#6                 |
| SEG task  |                                     |
| OFF task  | INT call---                         |
| AX        | pusha---CPU SP#5                    |
| CX        |                                     |
| BX        |                                     |
| SP        | ->AX                                |
| BP        |                                     |
| SI        | pusha---                            |
| DI        |                                     |
| ES        | ->StkPtr,<br>push es 필요<br>CPU SP#4 |
| from RunQ | LO-MEM                              |

#### Fake Stack

>Process 시작 직후 interrupt가 일어나면 process를 위한 fake stack을 만들어줘야 한다.

| StkPtr      | Properties                                  |
| ----------- | ------------------------------------------- |
|             | OS-PCB                                      |
|             | HI-MEM                                      |
| void \*data | arg for process                             |
| SEG task    |                                             |
| OFF task    |                                             |
| PSW         | INT call---CPU SP#1<br>interrupt-enable     |
| SEG task    |                                             |
| OFF task    | INT call---                                 |
| AX          | pusha---CPU SP#2                            |
| CX          |                                             |
| BX          |                                             |
| SP          | ->AX                                        |
| BP          |                                             |
| SI          | pusha---<br>레지스터 내부 값은 필요한 경우 제외 채울 필요는 없다. |
| ES          | ->StkPtr,<br>push es 필요<br>CPU SP#3         |
|             | LO-MEM                                      |

## 4. Process Creation and Termination

### Process Creation

#### full-fledged OS에서 새로운 process 생성

- Scratch에서 하나를 build
	- Process 0
- 존재하는 것을 clone
	- fork() syscall

#### From Scratch

>Process 첫 생성

1. Memory에서 code와 data 불러오기
2. (empty) Call stack 생성.
3. PCB 만들고 초기화.
4. ReadyQ에 process 집어넣기.

#### Cloning

>Parent가 fork() syscall로 child 생성 > PID를 제외한 context 복사.

1. 진행 중인 process를 멈추고 state를 저장.
2. PID 제외한 context를 복사.
3. 새로운 process를 ReadyQ에 넣기.

#### Unix에서 process의 life-cycle

![process_life_cycle](public/img/process_life_cycle.png)

- Parent는 wait() 함수로 child의 종료를 기다림.
- Child는 exit-status를 남겨 parent가 access할 수 있도록 한다.

#### Copy Status??

- fork() 해서 states를 copy할 때 두 경우를 생각할 수 있다.
	- Deep copy
	- Shallow copy
- Deep copy는 state를 모두 복사해 새로운 stack을 만든다.
	- Resource 낭비가 심하다!
- Shallow copy는 stack pointer를 복사해 넘긴다.
	- 참조 후 write해야 하면 hard-copy한다!
	- Interrupt해 kernel code 작동.

### Process Termination

- exit()
	- Child가 parent에 exit status를 넘길 때 사용한다.
	- Process의 memory allocate를 해제한다.
- abort()
	- Parent가 child를 terminate 시킨다.
	- Child가 할당된 resource를 초과했을 때 수행.
	- Task가 child를 더 이상 필요로 하지 않을 때.
	- Parent가 살아있어야 한다.

## 5. Multithreading

>Process는 독립적 segments를 가지고 있다.\
>\> 병렬 연산을 위해 process를 늘린