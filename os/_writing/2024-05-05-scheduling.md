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