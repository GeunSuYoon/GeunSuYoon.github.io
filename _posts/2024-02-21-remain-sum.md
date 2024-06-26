---
layout: post
categories:
  - boj
title: "[BOJ] 백준 나머지 합 10986"
date: 2024-02-21 20:16:00 +09:00
tags:
  - math
---
# [BOJ] 백준 나머지 합 10986

>[백준 10986. 나머지 합](https://www.acmicpc.net/problem/10986)의 풀이이다.

![subject](/public/img/boj_remainsum_subject.png)

- 길이 n의 배열에서 부분합이 m으로 나누어 떨어지는 개수를 출력하는 문제.

## 문제 풀이
- 입력이 예제와 같이 들어온다고 하자(n = 5, m = 3).
	>`5 3`
	>
	>`1 2 3 1 2`
- 배열을 A, 누적합을 S, S\[i]를 m으로 나눈 나머지를 M으로 표현하면 아래 표와 같이 나온다.

| index | 0 | 1 | 2 | 3 | 4 |
| ---- | ---- | ---- | ---- | ---- | ---- |
| `A[i]` | 1 | 2 | 3 | 1 | 2 |
| `S[i]` | 1 | 3 | 6 | 7 | 9 |
| `M[i]` | 1 | 0 | 0 | 1 | 0 |

- 이를 이용해 우린 M이란 배열의 값을 세는 mod란 배열을 만들면 아래와 같이 나온다.

| index | 0 | 1 | 2 |
| ---- | ---- | ---- | ---- |
| `mod[i]` | 3 | 2 | 0 |

- 이 표에서 같은 index, 즉 동일한 나머지를 갖는 두 구간을 선택해 누적 합을 뺀다면 나머지는 0이 될 것이다.
	<!-- - 나머지가 i인 구간을 2개 뽑는 경우의 수는 mod\[i] * (mod\[i] - 1) / 2 이다. ([조합](2024-02-21-permuncomb.md)) -->
	- 물론 mod\[i]의 값이 0인 경우엔 세지 않는다.
		- i = 0, 3 * 2 / 2 = 3
		- i = 1, 2 * 1 / 2 = 1
- 또한, 원래부터 나머지가 0인 구간을 세어주면 누적 합을 m으로 나눈 나머지가 0이 되는 구간을 모두 찾을 수 있다.
	- mod\[0] = 3.
	- 3 + 3 + 1 = 7
