---
layout: post
categories:
  - platform
title: "[Platform] Databricks"
date: 2024-05-12 05:57:00 +09:00
tags:
---
# \[Platform] Databricks

>최근 AI의 발전으로 많은 사람들이 이를 활용한다.\
>DB에 AI기술을 접목시킨 Databricks에 대해 알아보자!

- Databricks는 Data와 AI를 동시에 다루는 회사다.
- 즉, Data를 AI를 활용해 처리한다!

## Data Analytics Architecture

### Delta Lake

- Data management에 활용하는 기술이다.
- 데이터의 직접적인 이동 없이 cloud, region, data platform 전반에 걸쳐 함께 작업할 수 있다.
	- 개방적이고 안전한 공유가 가능하다!
	- 수신자가 관련된 platform, cloud를 이용하지 않아도 공유할 수 있다!!

### Apache Spark

- 오픈소스다.
- 범용 목적을 지닌 분산 클러스터 컴퓨팅 프레임워크이다.
- 일종의 통합 컴퓨팅 엔진으로 볼 수 있다.
- 클러스터 환경에서 데이터를 병렬로 처리하는 라이브러리 집합이다.
- SQL 뿐만 아니라 스트리밍, 머신러닝도 지원한다!
- 이런 특성을 이용해 빅데이터 처리를 쉽게 할 수 있고, 클러스터 확장성도 뛰어나다.
	- 즉, 빅데이터 처리를 위한 오픈소스 분산 차리 플랫폼, 빅데이터 분산 처리 엔진으로 볼 수 있다!!
- Databricks는 이 Apache Spark를 이용해 대규모 데이터를 처리할 수 있다!

### Data Science Workspace

- Control Plane에 존재하는 모든 Databricks Network에 접근할 수 있는 환경이다.
- 주요 객체는 아래와 같다.

#### Notebooks

- 명령어, 시각화, 텍스트 등을 포함한 문서에 대한 웹 기반 인터페이스

#### Dashboard

- 시각화 제공 인터페이스

#### Library

- 클러스터에서 실행되는 노트북, job 등에서 사용 가능한 코드 패키지이다.
- 커스텀이 가능하다.

#### Repo

- Git repository에 동기화 되어 관리되는 컨텐츠.
