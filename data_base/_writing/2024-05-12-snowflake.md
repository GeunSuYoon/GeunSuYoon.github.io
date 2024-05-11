---
layout: post
categories:
  - data_base
title: "[DB] Snowflake"
date: 2024-05-12 06:23:00 +09:00
tags:
---
# \[DB] Snowflake

>Cloud기반 Data solution Platform.

- 데이터 저장, 처리, 시각화 그리고 머신러닝까지 한번에 할 수 있는 클라우드 기반 통합 데이터 플랫폼.
- 데이터 클라우드 플랫폼 내에서 데이터 편집, 이동이 자유롭고, 저장 및 보관을 효율적으로 할 수 있다!

## Architecture

### Self-managed Service Data Platform

- 따로 설치하거나 관리할 물리적 하드웨어, 소프트웨어가 존재하지 않는다.
	- 완전히 Cloud Infra에서 실행된다.
	- 가상 컴퓨팅 instance를 사용하고, 데이터를 영구 저장 하기 위해 Storage Service를 사용한다.
- 지속적인 유지 및 관리를 Snowflake에서 알아서 처리한다.

### Snowflake Architecture

![snowflake_arch](/public/img/snowflake_arch.png)

## Cloud Platform

- 이하 Cloud Platform에서 호스팅 될 수 있다.
	1. AWS
	2. GCP
	3. Azure