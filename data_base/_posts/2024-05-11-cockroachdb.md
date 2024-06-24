---
layout: post
categories:
  - data_base
title: "[DB] CockroachDB"
date: 2024-05-11 13:51:00 +09:00
tags:
---
# \[DB] CockroachDB

>데브시스터즈의 대표 게임 중 하나 '쿠키런 킹덤'은 CockroachDB를 사용한다.\
>이 DB에 대해 알아보자!

- Cockroach Labs에서 개발한 상용 분산 SQL DB 관리 시스템이다.
- 데이터 센터 오류를 견딜 수 있는 transaction과 일관된 key-value 저장소 위에 구축돼 있다.
- 수평으로 확장이 가능하다.
- 데이터 센터 오류에 강해 cockroach, 바퀴벌레라는 이름을 따왔다!

## CockroachDB 특징

### PostgreSQL Compatibiliity

- PostgreSQL은 오픈소스 ORDBMS이다.
- MySQL에 비해 SQL 표준을 더 잘 지원하고 기능이 강력하며, 쿼리가 복잡할수록 성능이 더 좋아진다.
- 이런 PostgreSQL 프로토콜 대부분을 지원해 기존 커뮤니티에 존재하던 다양한 DB 접속 라이브러리나 ORM 등을 거의 그대로 사용할 수 있다. (RDB)

### Serialization Transaction

- SQL 표준에 정의된 Transaction 격리 수준 4단계 중 가장 강력한 Serializable 격리를 모든 transaction에서 사용하도록 되어 있다.
- 여러 transaction을 동시에 실행해도 한 번에 하나씩 실행한 것과 같은 결과를 보장한다!

### 수평 확장성

- DM 확장이 필요한 경우 노드를 추가로 확보한 뒤 붙여주기만 하면 된다.
	- 처리량과 용량이 그대로 늘어난다!
- 노드를 확장이나 축소, 교체할 때 서비스 중단 없이 작업할 수 있다.

### Multi-Region 클러스터 지원

- DB를 쪼개거나 shading 하지 않고 하나의 클러스터를 여러 개의 region에서 운영할 수 있다.
	- 여러 region에 물리적으로 DB를 나눌 필요가 없다!
	- 물리적으로 나눈 DB의 sync 문제도 해결할 수 있다!!!
