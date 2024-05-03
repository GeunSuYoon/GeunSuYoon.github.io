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
	- 