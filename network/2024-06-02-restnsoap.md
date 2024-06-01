---
layout: post
categories:
  - network
title: "[Net] REST and SOAP"
date: 
tags:
---
# \[Net] REST and SOAP

## REST API

- REpresentational State Transfer
- 네트워크를 통해 컴퓨터 간 통신을 할 수 있게 해주는 아키텍처 스타일.
- 인터넷 식별자(URI)와 HTTP 프로토콜을 기반으로 한다.
- 슈퍼 브라우저와 호환되는 데이터 형식에 JSON을 사용한다.

### 특징

- HTTP 프로토콜을 사용하므로 간단하다.
- 클라이언트 - 서버 통신 및 아키텍처를 용이하게 한다.
- 단일 균일 인터페이스를 사용한다.
	- 해당 API를 사용하는 애플리케이션들이 동일한 경로를 통해 접속해야 함.
- 웹에 최적화 되어있다.
- 확장성이 좋다.

## SOAP API

- Simple Object Access Protocol
- 이 자체로 프로토콜이다.
- 보안이나 메세지 전송 등에 더 많은 표준들이 정해져 있어 조금 복잡하다.
	- 오버헤드가 커진다.

### 특징

- 보안이 더 엄격하다.
	- 기업용으로 적합함.
- 안정적 메시징을 위해 원자성(atomic)을 가진다.
- ACID 준수가 내장돼 있다.

## API간 차이점

- REST는 아키텍처 스타일, SOAP는 프로토콜이다.
- REST는 URI에 접근, SOAP는 작업을 수행한다.
- 보안 방법이 다르다.
- REST는 적은 리소스, SOAP는 더 많은 대역폭을 요구한다.
- REST 호출은 cache 가능, SOAP 호풀은 cache 불가능.