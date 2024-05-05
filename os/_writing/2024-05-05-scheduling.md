---
layout: post
categories: 
title: "[Lecture - OS] 05. Scheduling"
date: 2024-05-05 16:10:00 +09:00
tags:
---
# \[Lecture - OS] Scheduling

>simple explane

## Agenda

1. Basic Concepts
2. Scheduling Policies
3. Fair Share Scheduling os Linux
4. Summary

## 1. Basic Concepts

### Resource Scheduling in General

#### Resources fall into two classes

- Preemptible
	- Resource를 뺏어 사용한 뒤 돌려줄 수 있다.
	- Ex: Processor or Disk
- Non-preemptible
	- Resource를 한 번 받으면 process가 돌려줄 때까지 사용할 수 없다.
	- Ex: File space, Terminal

#### OS는 resource에 대해 두 가지 결정을 내려야 한다.

- 누가 다음에 쓸 것인가?
- 얼마나 오래 쓰게 할 것인가?

### Entities Involved in Scheduling

#### Multiprogramming

- OS는 여러 개의 process를 memory에 load할 수 있다.
- 해당 process들은 CPU를 time-multiplexing으로 공유한다.

### CPU Burst

>최신 OS에서 CPU scheduling할 때 참고하는 entity다.

#### CPU-I/O Burst Cycle

- Process execution은 CPU execution과 I/O wait의 cycle로 이루어져 있다.
- CPU execution과 I/O wait time을 비교해 CPU-I/O Bound/Intensive process로 구분할 수 있다.
	- CPU intensive는 throughput이 중요하다.
	- I/O intensive는 반응 속도가 중요하다.

### CPU Scheduler

>Ready 상태인 memory 내 process를 선택한 뒤, CPU에 해당 process를 할당해야 한다. 어떤 방법으로?

#### CPU Scheduling은 아래의 경우에 process를 선택한다.

1. Switches from running to waiting state
2. Switches from running to ready state
3. Switches from waiting to ready state
4. Terminates
- 1과 4는 non-preemptive다.
- 다른 것들은 preemptive다.

#### Process는 세 가지 scheduling state를 가진다.

- Running
	- CPU 보유
- Ready
	- CPU 주세요
- Waiting(Blocked)
	- 특정 event를 기다린다.(disk I/O, message, semaphore, etc.)

![process_state_transition](/public/img/process_state_transition.png)

- Running to Waiting은 non-preemptive

### Dispatcher

#### Dispatcher는 scheduler에 의해 선택된 process에게 CPU control을 넘긴다.
- Switching Context
- Switching to user mode
- 다시 시작한 program이 이전까지 진행하던 곳으로 jump

#### Latancy

- Dispatcher가 한 process를 멈추고 다른 것을 시작하는데 걸리는 시간

## 2. Scheduling Policies

>어떤 process를 선택할 것인가\
>얼마나 process를 동작할 것인가

### Scheduling Objectives

#### Resourc utilization 최대화

- CPU와 I/O device를 최대한 사용해야 한다.

#### Overhead 최소화

#### Context Switch 최소화

#### CPU cycle 공정 분배

### Optimization Metrics

#### Throughput

- 시간 단위 당 끝낼 수 있는 process의 숫자

#### Turnaround time

- 특정 process를 종료하는 시간

#### Waiting time

- Process가 ReadyQ에 있는 시간

#### Response time

- 첫 response 제출 후 request 생성까지 걸리는 시간.

### Scheduling Policies

>CPU scheduler가 사용하는 것들.


#### 규칙

- FIFO(FCFS), RR, SJF, MLFQ(EQ), etc.

### FIFO (First In First Out)

>Non-preemptive programming\
>First Come First Served (FCFS)로도 불린다.

#### Key ideas

- 처음 온 애를 끝날 때 까지 돌리자. (CPU 독점 > time interrupt로 해결)
- 가장 간단하다. Uniprogramming이다.
- Finished는 Blocked를 의미한다.
	- 하나의 process가 CPU 사용하는 동안 다른 것들은 semaphore에서 대기.
	- Ready일 때 RunQ로 돌아감.
- 문제점
	- 하나의 process가 CPU를 독점한다.
- 해결법
	- Context switch를 제외하고 최대 동작 시간을 제한한다.
	- 이 시간을 "Time slice"라고 부른다.

#### 예시

- 아래와 같은 특징을 가진 process들이 있다고 하자.

| -Process- | -Burst Time- |
| --------- | ------------ |
| $P_1$     | 24           |
| $P_2$     | 3            |
| $P_3$     | 3            |

- 아래와 같은 Gantt Chart를 생각해보자.

![gantt_chart_1](/public/img/gantt_chart_1.png)

- Waiting time
	- $P_1$ = 0
	- $P_2$ = 24
	- $P_3$ = 27
- Average waiting time: (0 + 24 + 27) / 3 = 17

- 다른 Gantt Chart를 보자.

![gantt_chart_2](/public/img/gantt_chart_2.png)

- Waiting time
	- $P_1$ = 6
	- $P_2$ = 0
	- $P_3$ = 3
- Average waiting time: (6 + 0 + 3) / 3 = 3

- Convoy Effect가 발생한다.
	- Burst time이 짧은 애들이 앞에 올 수록 AWT가 짧아짐!!!

### SJF (Shortest Job First)

#### Key operation

- 각 process의 다음 CPU burst에 따라 짧은 것을 먼저 실행.

#### Optimal

- 