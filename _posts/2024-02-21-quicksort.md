---
layout: post
title: "[Algorithm] Quick Sort"
date: 2024-02-21 18:30:00 +09:00
categories:
  - algorithm
tags:
  - sort
---
# [Algorithm] 퀵 정렬 (Quick Sort)

- 안전 정렬 : 동일한 값에 기존 순서가 유지(버블, 삽입)
- 불안정 정렬 : 동일한 값에 기존 순서가 유지X(선택, 퀵)

## 시간복잡도
- 평균 : O(nlogn)
- 최악 : O(n^2)

## 장단점
### 장점
- 불필요한 데이터 이동을 줄이고 먼 거리의 데이터를 교환, 사용한 pivot을 이후 연산에서 제외하므로 시간복잡도 O(nlogn)을 가지는 다른 알고리즘보다 빠름.
- 다른 메모리 공간 필요 X
### 단점
- 불안정 정렬
- 이미 정렬된 경우 O(n^2) 시간이 걸림.

## 구현 방법

### Pivot 선택
- 첫 번째, 중간, 마지막, 랜덤
- 선택 방식에 따라 속도가 달라진다!

## 구현 내용

### quickSorting(int[] arr, int left, int right)
- left <= right ? return ; //탈출 조건
- int part = partition(arr, left, right); //정렬 후 pivot idx.
- quickSorting(arr, left, part - 1); //pivot보다 작은 부분 정렬.
- quickSorting(arr, part + 1, right); //pivot보다 큰 부분 정렬.

### partition(int[] arr, int left, int right)
- mid = (left + right) / 2; //중간 값이 pivot의 idx
- pivot = arr\[mid];
- swap arr\[left] and arr\[mid]; //pivot을 제일 왼쪽으로
- smallCnt = left, bigCnt = right; //작은 것을 왼 쪽에, 큰 것을 오른쪽에
- while smallCnt < bigCnt
	- while arr\[smallCnt] < pivot
		- smallCnt++; //pivot보다 큰 값을 찾을 때 까지 idx 증가.
	- while pivot < arr\[bigCnt]
		- bigCnt++; //pivot보다 작은 값을 찾을 때 까지 idx 감소.
	- swap arr\[smallCnt] and arr\[bigCnt] //작은 값을 왼쪽에, 큰 값을 오른쪽에.
- return smallCnt; //현재 pivot 위치를 반환.
