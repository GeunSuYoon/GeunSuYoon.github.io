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


### 수평 확장성


### Multi-Region 클러스터 지원

