---
layout: post
title: "Hash Table"
date: 2024-02-20 20:51:54 +09:00
categories: [data_structure]
tags: [data_structure]
---
# Hash Table
- 브루트포스(완전 탐색, O(n^2))로 시간 초과에 빠지게 되는 문제에 사용.

### 각 값의 의미

#### HashTable\[HASH_SIZE]\[HASH_LEN]
- 테이블을 2차원 배열로 구현해 해당 값을 key를 이용해 몇 번 중복해서 들어왔는지 저장한다.

#### TableLen\[HASH_SIZE]
- 들어온 key값을 저장할 index를 담고 있는 배열.
- 즉, 0이면 바로 넣지만 0이 아니면 Data를 돌면서 일치하는 값이 있는지 찾는 역할을 한다.

#### Data\[HASH_SIZE]\[HASH_LEN]
- 테이블에 실제로 들어간 값을 저장한다.
- HASH_LEN 부분의 인덱스는 TableLen\[HASH_SIZE]이다.

#### HASH_SIZE
- 2차원 배열로 구현하는데, 그 중 colum을 담당.

#### HASH_LEN
- 2차원 배열의 row를 담당.
- 중복해서 들어올 수 있는 key의 개수라고 생각하면 편하다.

#### HASH_VAL
- key 값을 만들 때 이용하는 값.
- 최대한 중복을 피하기 위해 소수(19, 23,29 등)를 이용하는 것이 좋다.
#### key
- 들어오는 데이터를 이용해 key 값을 만든다.
- HASH_VAL과 자신만의 방법을 이용해 값을 만들고, HASH_SIZE로 나눈 몫을 출력한다.
- 음수면 -1을 곱해 양수로 만들어준다.

### 함수 내용

#### getHashKey
- 위의 내용을 토대로 HASH_VAL을 이용해 key값을 만든다.

#### isExist
- key값을 이용해 TableLen\[key]의 값을 조사.
	- 만약 0이면 Data\[key]\[TableLen\[key]]에 저장하고, Length\[key]의 값을 1 증가.
	- 0이 아니면 Data\[key]\[cnt = 0 to TableLen\[key]]를 돌며 일치하는 데이터가 있는지 확인한다.
		- 만일 중복되는 값이 있으면 HashTable\[key]\[cnt]값을 1 늘리고 해당 값 반환.
	- Data\[key]\[TableLen\[key]]에 저장하고, TableLen\[key]의 값을 1 증가.
	- 0 반환.
