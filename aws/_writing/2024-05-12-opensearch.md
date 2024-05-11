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
- 대시보드 인터페이스와 REST API를 사용해 알림을 구성하고 관리할 수 있다.
	- 여러 SNS 시스템을 이용해 알림을 수신할 수 있다.
- Amazon CloudWatch를 이용해 추가 비용 없이 여러 지표를 확인할 수도 있다!

### 오픈 소스 도구 통합

- 필요한 오픈 소스 도구를 사용해 데이터 수집 및 시각화가 가능하다.

### Vector Search

- 기계 학습을 이용해 비정형 데이터의 의미와 context를 숫자로 표현하는 방법이다.
	- 이를 통해 비정형 데이터 사이 유사성을 확인할 수 있다!
- 다만, OpenSearch에서 Vector Search를 사용하면 메모리 절반을 검색 엔진(ElasticSearch), 나머지 절반을 Vector Search에 사용하도록 구성됭