---
layout: post
categories:
  - aws
title: "[AWS] OpenSearch"
date: 2024-05-12 07:50:00 +09:00
tags:
---
# \[AWS] OpenSearch

- AWS에서 제공하는 OpenSearch는 오픈 소스이다.
	- 따라서 AWS에서만 사용 가능한 것이 아니라 직접 구축해서 사용할 수 있다!
- 검색 엔진 기능 및 Vector Search 기능도 제공한다.
	- 검색 엔진은 Elastic Search를 활용한다.

## OpenSearch 특징

### 쿼리 다중 언어 지원

- 쿼리 도메인별 언어 숙련도가 필요하지 않다.
- SQL로 작성하거나 PPL(파이프 처리 언어, 파이프('|') 사용을 지원)을 이용해 쿼리할 수 있다.

### 이벤트 모니터링 및 알림

- 클러스터에 저장된 데이터 모니터링, 미리 구성한 임계값에 따라 알림을 자동으로 전송 가능.
- 대시보드 인터페이스와 RE

### 오픈 소스 도구 통합
