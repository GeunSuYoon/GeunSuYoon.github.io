---
layout: post
title: "[Algorithm] Bubble Sort"
date: 2024-02-20 20:44:23 +09:00
categories:
  - algorithm
tags:
  - sort
---
# \[Algorithm] 거품 정렬

>각 index를 비교하며 가장 마지막, 혹은 가장 앞에서부터 순서대로 배치한다.
>
>구현이 단순하나 비효율적이다.

#### 시간 복잡도
- O(n^2)

### 과정
- 구현마다 다르나 오름차순으로 바로 옆 index끼리 비교하는 것으로 한다.
- 배열 arr이 n의 크기를 가진다 하자.
- k = 0 to n -1까지 도는 loop를 만든다.
	- 그 내부에 l = n to k + 1까지 도는 loop를 만든다.
	- arr\[l]과 arr\[l - 1]의 값을 비교해 swap하거나 넘어간다.
- 그러면 k번째 index의 값이 가장 작은 값이 남게 된다.