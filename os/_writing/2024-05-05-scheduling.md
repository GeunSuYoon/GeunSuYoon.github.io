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

### CPU 