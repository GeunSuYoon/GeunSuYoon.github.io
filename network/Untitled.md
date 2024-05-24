---
layout: post
categories:
  - network
title: "[Network] ACID와 BASE"
date: 2024-05-24 16:54:00 +09:00
tags:
---
# \[Network] ACID와 BASD

>DB 트랜잭션 처리를 위한 개념이다.

## ACID

- 안전하고 신뢰 가능한 트랜잭션을 보장한다.

### 원칙

#### Atomicity (원자성)

- 단일 트랜잭션은 단계가 완료 되거나 원래 상태로 돌아가야 한다. (execute or abort)
- 트랜잭션 일부만 실패해도 데이터는 변경되지 않는다.

#### Consistency (일관성)

- 여러 사용자가 동시에 유사한 작업을 수행하더라도 모든 사용자는 일관된 데이터를 유지한다.
	- 은행 계좌 이체할 때와 비슷하다고 생각하면 된다.

#### Isolation (격리성)

- 새 트랜잭션은 이전 트랜잭션이 완료될 때까지 기다린다.
- 트랜잭션이 서로 간섭하지 않도록 보장해 순차적으로 실행되는 것처럼 보인다.

#### Durability (내구)

- 시스템에 오류가 생겨도 commit된 모든 기록은 DB에 유지한다.

## BASE

### 원칙

#### Basically Available

- 사용자가 언제든 DB에 동시에 접근할 수 있다.
	- 이전 사용자가 완료될 때까지 기다릴 필요가 없다.

#### Soft-state

- 데이터가

#### Eventually consistent