---
layout: post
categories:
  - algorithm
  - tree
title: "[Algorithm] Binary Search"
date: 2024-02-21 18:36:00 +09:00
tags:
  - tree
  - search
---
# \[Algorithm] 이진 탐색

### 이진 탐색(이분 탐색)
- 처음부터 끝까지 돌면서 탐색하기 보단 탐색 범위를 두 부분으로 나눠 분할해서 찾는 방식.
- 이미 정렬된 배열에서 특정 값을 찾을 때 빠르게 찾을 수 있다.

### 시간 복잡도
- O(logn)

### 진행 순서
- 우선 배열을 정렬 (해당 배열을 arr이라 하겠음)
- 0을 left, arr.len을 right로 설정. mid = (left + right) / 2;
- mid번째 인덱스의 값과 비교하며 목표(target)에 대해 아래 과정 반복
	- left > right ? return $fail(-1 or something)
	- arr[mid] == target ? return target or mid;
	- arr[mid] < target ? right = mid - 1;
	- arr[mid] > target ? left = mid + 1;
