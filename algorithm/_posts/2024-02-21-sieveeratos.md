---
layout: post
categories:
  - algorithm
  - math
title: "[Algorithm] Sieve of Eratosthenes"
date: 2024-02-21 19:14:00 +09:00
tags:
  - math
---
# \[Algorithm] 에라토크테네스의 체

>에라토크테네스의 체.

- 소수를 찾는 방법.
- 체로 수를 거르는 것 같다 하여 이런 이름이 붙었다.

## 방법
- 1~n까지 숫자 중 소수를 찾는다고 하자.
- 숫자를 쭉 쓰고 1을 제거한다.
- 2를 제외한 2의 배수 제거
- 3을 제외한 3의 배수 제거
- ...
- 소수인 m(m < sqrt(n))을 제외한 m의 배수 제거

## 구현 방법 (c)
- let MAX = 1000001
- prime\[MAX] = {0, };
- change_bool(int start, int acc, int flag)
	- for cnt = start; cnt < MAX; cnt += acc
		- prime\[cnt] = flag;
- prime\[2] = 1; // 2는 소수
- prime\[3] = 1; // 3은 소수. 나머지 홀수만 판별하자!
- change_bool(5, 6, 1); // 5 mod 6 참으로 설정. 
- change_bool(7, 6, 1); // 1 mod 6 참으로 설정. 1은 소수가 아니므로 7부터.
- // 위의 두 집합은 2의 배수도, 3의 배수도 아닌 숫자 집합!
- for prime_cnt = 5; prime_sq = 25; prime_sq < MAX
	- nxt = (prime_cnt - 3) % 6 // prime_cnt가 5 mod 6이면 2, 1 mod 6이면 4
	- if (prime\[prime_cnt] == 1) //현재 숫자가 소수?
		- add_cnt = prime_cnt * 6 // prime_cnt mod 6만 검사
		- change_bool(prime_sq, add_cnt; 0) // prime_cnt^2 미만 숫자는 소수로 판별 됐음. prime_cnt^2 이상의 숫자만 판별.
		- change_bool(nxt * prime_cnt + prime_sq, add_cnt, 0) // prime_cnt(primr_cnt + nxt) 부터
- prime_cnt += nxt
- prime_sq = prime_cnt * prime_cnt