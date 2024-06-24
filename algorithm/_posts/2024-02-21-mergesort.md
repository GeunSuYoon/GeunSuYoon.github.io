---
layout: post
categories:
  - algorithm
title: "[Algorithm] Merge Sort"
date: 2024-02-21 18:34:00 +09:00
tags:
  - sort
---
# \[Algorithm] 병합 정렬 (Merge Sort)

>병합 정렬.
>
>Divide and Conquer(분할 정복) 방법을 이용해 구현.
>
>안정 정렬에 속한다.

## 시간복잡도
- O(nlogn)

## [QuickSort](2024-02-21-quicksort.md)와 차이점
- QS
	- Pivot을 통해 정렬(partition) > 영역을 쪼갬
	- Pivot을 임의로 정하므로 LinkedList에서는 불가.
- MS
	- 영역을 쪼갤 수 있는 만큼 쪼갬 > 정렬
	- LinkedList에서 효율적.

## 장단점

### 장점
- 데이터 분포에 영향을 덜 받는다. > 입력 데이터가 무엇이던 간에 시간 동일
- 크기가 큰 레코드를 정렬한 경우, LinkedList를 사용하면 어떤 정렬 방법보다 효율적.
- 안정 정렬
### 단점
- 레코드를 배열로 구성하면 임시 배열이 필요
	- 메모리 낭비
	- 제자리 정렬이 아님
- 레코드 크기가 크면 이동 횟수가 많아 큰 시간 낭비

## 구현 내용

### mergeSort(int[] arr, int left, int right)
- right <= left ? return ;
- mid = (left + right) / 2; //중앙값
- mergeSort(arr, left, mid); //중앙 기준 왼쪽
- mergeSort(arr, mid + 1, right); //중앙 기준 오른쪽
- merge(arr, left, mid, right); //병합

### merge(int[] arr, int left, int mid, int right)
- leftLen = mid - left + 1, rightLen = right - mid, totalLen = right - left + 1; //나누고 합칠 길이
- arrCnt = leftCnt = rightCnt = 0; //각 배열 인덱스
- leftArr = copy arr from left to mid, rightArr = copy arr mid + 1 to right; //배열 절반씩 복사
- while arrCnt = 0 to totalLen - 1
	- while leftCnt = 0 to leftLen - 1 and rightCnt = 0 to rightLen - 1 //양쪽 모두 복사 덜 됨
		- leftArr\[leftCnt] < rightArr\[rightCnt]
			- ? arr\[left + arrCnt] = leftArr\[leftCnt++]; //왼쪽이 작으면 leftArr 요소 복사
			- : arr\[left + arrCnt] = rightArr\[rightCnt++]; //오른쪽이 작으면 rightArr 요소 복사
		- arrCnt++;
	- leftLen == leftCnt
		- ? copy remain factors in rightArr to arr //왼쪽 복사 끝났으면 남은 오른쪽 요소 복사
		- : copy remain factors in leftArr to arr //오른쪽 복사 끝났으면 남은 왼쪽 요소 복사