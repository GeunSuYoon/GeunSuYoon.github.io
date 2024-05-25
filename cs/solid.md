---
layout: post
categories:
  - cs
title: "[CS] SOLID 원칙"
date: 2024-05-24 17:46:00 +09:00
tags:
---
# \[CS] SOLID 원칙

>객체 지향 프로그래밍 설계의 다섯 가지 기본 원칙

## Single responibility principle (단일 책임 원칙)

- 하나의 클래스는 하나의 책임만 가져야 한다.

## Open/closed principle (개방-폐쇄 원칙)

- 개체는 확장에 대해 열려 있어야 하고, 수정에 대해 닫혀 있어야 한다.
	- 개체를 상속 받는 개체는 동작(추상화)은 변경할 수 있다.
		- 기존 코드 
	- 하지만, 개체 자체를 수정할 수는 없다.

## Liskov substitution principle

- 자료형 S가 자료형 T의 서브타입일 때, 속성 변경 없이 T를 S로 교체할 수 있어야 한다.
	- 서로 교체했을 때, 무리 없이 작동해야 한다.
	- 즉, 자료형을 만들 때 모든 경우를 고려해 만들어야 한다.

## Interface segregation principle

- 클라이언트가 자신이 용하지 않는 메소드에 의존하지 않아야 한다.
	- 하나의 큰 메소드가 아닌 여러 개의 작은 메소드로 분리하는 것이 좋다.

## Dependency inversion principle

- 추상화에 의존해야 하고, 구체화에 의존해선 안된다.
	- 상위 모듈은 하위 모듈에 의존해선 안된다. 두 모듈 전부 추상화에 의존해야 한다.
	- 추상화는 세부 사항에 의존해선 안된다. 세부 사항이 추상화에 의존해야 한다.