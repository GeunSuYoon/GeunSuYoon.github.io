---
layout: post
categories:
  - algorithm
title: "[Algorithm] Counting Sort"
date: 2024-02-21 19:17:00 +09:00
tags:
  - sort
---
# \[Algorithm] 계수 정렬 (Counting Sort)

>n개의 원소 배열을 정렬하는 가짓수는 n!
>
>해당 방법으로 만든 트리의 말단 노드가 n! 이상이 되기 위해선 2^h >= n!을 만족하는 h를 가지고 h > O(nlogn)을 만족.(h는 트리의 높이)
>
>O(nlogn)을 줄일 수 있는 방법은 Comparison을 하지 않는 것!

- counting이 필요하다!(각 숫자가 몇 번 등장했는지 센다)
- 정렬하는 배열이 특정 범위 내에 있을 때 사용한다.

#### 시간복잡도
- O(n + k) ,k는 배열에서 나오는 최댓값
#### 공간복잡도
- O(k) ,k개의 배열을 만들어야 함.

### 장단점
#### 장점
- O(n)의 시간 복잡도
#### 단점
- 메모리 낭비가 심함.
### 구현 방법
- arrLen = arr.len;
- returnArr\[arrLen]; //반환해줄 정렬된 배열
- countLen = max value in arr;
- count\[countLen];
- for cnt = 0 to arrLen - 1
	- count\[arr\[cnt]]++; //arr 안에 있는 값이 몇 번 등장했는지 카운트!
- for cnt = 1 to arrLen - 1
	- count\[cnt] += count\[cnt - 1]; //count를 누적합으로 만들어줘 index 위치를 특정!
- for cnt = arrLen - 1 to 0
	- returnArr\[count\[arr\[cnt]] - 1] = arr\[cnt];
	- count\[cnt]--;