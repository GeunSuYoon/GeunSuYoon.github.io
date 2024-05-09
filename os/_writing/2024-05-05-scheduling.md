---
layout: post
categories: 
title: "[Lecture - OS] 05. Scheduling"
date: 2024-05-05 16:10:00 +09:00
tags:
---
# \[Lecture - OS] Scheduling

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

- 주어진 set of processes의 AWT를 최소화 한다.

#### 두 가지 방법

- Non-preemptive
	- Process가 CPU를 가진 후, CPU burst 이전까지 독점
- Preemptive
	- 지금 동작하는 process보다 CPU burst가 더 짧은 process가 도착하면 그 즉시 교체.
	- SRTF(Shortest Remaining Time First) 혹은 STCF(Shortest Time to Completion First)라고 불린다.

#### 예시

- 아래와 같은 process들이 있다고 하자.

| -Process- | -Arrival Time- | -Burst Time- |
| --------- | -------------- | ------------ |
| $P_1$     | 0              | 7            |
| $P_2$     | 2              | 4            |
| $P_3$     | 4              | 1            |
| $P_4$     | 5              | 4            |

- Non-preemptive Gantt Chart
	
	![gantt_chart_sjf_non_preemptive](/public/img/gantt_chart_sjf_non_preemptive.png)
	
- AWT = (0 + 6 + 3 + 7) / 4 = 4

- Non-preemptive Gantt Chart
	
	![gantt_chart_sjf_preemptive](/public/img/gantt_chart_sjf_preemptive.png)
	
- AWT = (9 + 1 + 0 + 2) / 4 = 3

#### Challenge: 다음 CPU burst size 예측

- 추측할 수 있는 것은 길이 뿐이다.
	- 이전 CPU burst length를 EMA를 이용한 ES로 해보자.  
	- ES(Exponential Smoothing)
	- EMA(Exponential Moving Everage)
		- $τ_{n+1} = α*t_n + (1-α)*τ_n$
		- $τ_{n+1}$: 다음 CPU burst를 예측하기 위한 값
		- $t_n$: $n^{th}$ CPU burst의 실제 길이
		- $α(0<=α<=1)$: Smoothing factor. 값이 클수록 최근 값을 높게 반영.

### RR (Round Robin)

>FIFO를 preemptive하게 만들자!

#### Key idea

- Process를 time slice만큼 실행하자.
- 그리고 RunQ에 다시 넣는다.
- 모든 process는 CPU를 동일하게 할당 받는다.
- 대부분 system이 이와 비슷한 것을 사용한다!

#### Priority 참고

- 높은 priority를 가진 process를 먼저 실행.
- 같은 priority는 RR
- RunQ 내 더 크거나 같은 priority process 뒤에 넣는다.

#### Time Slice Selection

- Time Slice를 제대로 선택하지 않으면?
	- Too Long
		- Process의 CPU 독점
	- Too Short
		- Context switch overhead가 너무 커짐 > Interrupt 너무 잦다.
- Unix는 1s로 설정
	- 너무 길다!
- 최근 system은 1~10ms로 설정.

#### FIFO와 비교

- 아래와 같은 process들이 있다고 하자.

| -Process- | -Burst Time- |
| --------- | ------------ |
| $P_1$     | 10           |
| $P_2$     | 1            |
- FIFO Gantt Chart
	
	![gantt_chart_rr_fifo_1](/public/img/gantt_chart_rr_fifo_1.png)
	
	- AWT = 5

- RR Gantt Chart
	
	![gantt_chart_rr_rr_1](/public/img/gantt_chart_rr_rr_1.png)
	
	- AWT = 1

- 아래와 같은 process들이 있다고 하자.

| -Process- | -Burst Time- |
| --------- | ------------ |
| $P_1$     | 5            |
| $P_2$     | 5            |

- FIFO Gantt Chart
	
	![gantt_chart_rr_fifo_2](/public/img/gantt_chart_rr_fifo_2.png)
	
	- AWT = 2.5

- RR Gantt Chart
	
	![gantt_chart_rr_rr_2](public/img/gantt_chart_rr_rr_2.png)
	
	- AWT = 4.5
- Fair하나 AWT는 하향 평준화 된다.

#### FIFO vs. RR

- RR에서 Time Slice를 inf.로 보내면 FIFO와 똑같다.
- Time Slice = 0이면 GPS가 된다.
	- 실제로 구현할 수는 없다.
	- GPS(Generalize Process Sharing)는 ideal RR이다.

#### Right size of Time slice value

- I/O intensive인 $P_1$, CPU intensive인 $P_2$를 생각해보자.
	- $P_1$은 1ms동안 동작하고 I/O를 10ms동안 기다린다.
	- $P_2$는 waiting 없이 계속 동작한다.

##### Time Slice = 100ms

![rr_ts_100ms](public/img/rr_ts_100ms.png)

- $U_{CPU}$ = 100%
- $U_{IO}$ = 10 / 101 ~ 10%

##### Time Slice = 1ms

![rr_ts_1ms](public/img/rr_ts_1ms.png)

- $U_{CPU}$ = 100%
- $U_{IO}$ = 10 / 11 ~ 91%
- 겉보기엔 좋아 보이지만, $P_2$는 interrupt가 자주 걸린다.
	- $P_2$에 $P_1$보다 Time slice를 크게 주면 어떨까?

### MLFQ (Multi-Level Feedback Queue)

>위에서 언급한 process간 특징 차이를 이용해 time slice를 다르게 주자!

#### MLFQ에서 idea development

- STCF는 나쁘지 않게 동작하지만, 예측이 필요하다.
	- 과거 데이터로 미래 예측
	- 이는 곧 resource 낭비로 연결된다.
- Dispatcher의 priority mechanism을 오래 동작하는 process에 적용하자!
- CPU-I/O intensive process로 분류
	- I/O intensive process에 높은 priority 부여
	- CPU intensive process에 낮은 priority 부여
	- 낮은 prioirty process에 긴 time slice 부여.

#### MLFQ scheduling

- Exponential Queue scheduling라 부르기도 한다.
- 새로 RunQ에 들어온 process에 가장 높은 priority를 부여한다.
	- 새로운 process는 I/O intensive로 간주
- 만약 process가 blocking 없이 time slice동안 동작을 끝내지 못하면?
	- Priority 1 감소.
	- Time slice는 2배 상승.
	- Priority가 n일 때, time slice는 $2^n$만큼 부여한다.

### FSS (Fair Share Scheduling)

>Continous process가 등장함에 따라 필요해졌다.

#### FSS

- 각 process의 최근 CPU 사용 정도를 기록.
- 짧은 CPU time을 사용한 process에 높은 priority 부여.
- "Billing factors"를 바꿔 priority 조정 가능.

## 3. Fair Share Scheduling in Linux

>과거에 mininum reponse time을 기준으로 했다면 이제 user perception에 따라 판단하자!

### Formulation

#### Terminology

- $N$ : size of RunQ
- $Φ$ : Set of tasks
- $W(τ_i)$ : Weight of $i^{th}$ task
- $S_Φ$ : Weight sum of tasks
- $T_{τ_i}(t_1, t_2)$ : Ideal time slice of task between interval $t_1$ and $t_2$
- $C_{τ_i}(t_1, t_2)$ : Real time slice of task between interval $t_1$ and $t_2$

#### FSS의 목표

- 주어진 weight를 이용해 각 process에 적절한 resource 분배.
- CPU time when GPS
- $C_{τ_i}(t_1, t_2) = {W(τ_i)}/{S_Φ} * (t_2 - t_1)$
	- Time interval의 weight 비율.
	- $t_2 - t_1$이 작을수록 좋지만, 너무 작으면 overhead가 커진다.
		- overhead가 0이라 가정하면, interval = 0 -> GPS

### Fairness Measurement

#### CPU time lag

- $lag_{τ_i}(t) = C_{τ_i}(t_1, t) - {W(τ_i)} / {S_Φ} * (t - t_1)$
	- 실제 CPU time - GPS에서 CPU time
	- Positive lag : GPS보다 더 많은 시간 받음
	- Negative lag : GPS보다 더 적은 시간 받음
- 이런 lag를 모든 time interval에서 최소화 하자!

### WRR (Weighted Round Robin)

#### Key

- Time Slice
	- $TS_{τ_i} = W(τ_i) / {S_Φ} *$ round_robin_interval_period
- Time Slice를 이용한 GPS approximation
- 각 task에 weighted time slice 할당
- RR로 task를 schedule
	- 한 time slice 단위로 task 실행.
- 예시

| /     | -weight- | -Arrival Time(ms)- | -Service Time(ms)- |
| ----- | -------- | ------------------ | ------------------ |
| $τ_1$ | 4        | 0                  | 48                 |
| $τ_2$ | 2        | 0                  | 48                 |
| $τ_3$ | 1        | 0                  | 36                 |
| $τ_4$ | 1        | 24                 | 24                 |

- round_robin_interval_period = 28ms

| /        | -Time Slice(ms)- |     |
| -------- | ---------------- | --- |
| Time(ms) | 0                | 24  |
| $τ_1$    | 16               | 14  |
| $τ_2$    | 8                | 7   |
| $τ_3$    | 4                | 3.5 |
| $τ_4$    | 0                | 3.5 |

#### Evaluation

- Low Scheduling Overhead: O(1)
- 하지만, fairness guarantee가 약하다
	- Interval이 커지면 lag도 커진다!

### WFQ (Weighted Fair Queuing)

>WRR과 Time quantam(C)는 동일. w가 큰 task가 새치기 하는 것!

#### Key

- VT(Virtual Time)
	- $VT_{τ_i}(t) = C_{τ_i}(0, t) / W(τ_i)$
	- Weight에 따른 진행도 체크
- Preemptive tick period
	- Preemptive를 위해 scheduler가 확인할 time interval
- VFT (Virtual Finish Time)
	- $VFT_{τ_i}(t) = VT_{τ_i}(t + T) = VT_{τ_i}(t) + T / W(τ_i)$

### CFS (Completely Fair Scheduler)

