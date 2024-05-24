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

### 원칙

#### Atomicity (원자성)

- 단일 트랜잭션은 단계가 완료 되거나 원래 상태로 돌아가야 한다. (execute or abort)
- 트랜잭션 일부만 실패해도 데이터는 변경되지 않는다.

#### Consistency (일관성)

- 여러 사용자가 동시에 유사한 작업을 수행하더라도 모든 사용자는 일관된 데이터를 유지한다.
	- 은행 계좌 이체할 때와 비슷하다고 생각하면 된다.

#### Isolation (격리성)

- 
- 트랜잭션이 서로 간섭하지 않도록 보장해 순차적으로 실행되는 것처럼 보인다.

#### Durability (내구)

## BASE

### 원칙