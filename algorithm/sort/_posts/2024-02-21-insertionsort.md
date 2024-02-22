---
layout: post
categories:
  - algorithm
title: Insertion Sort
date: 2024-02-21 18:31:00 +09:00
tags:
  - sort
---
# Insertion Sort
>해당 index에 있는 원소를 앞에 정렬된 원소의 값과 비교해 적절한 위치를 찾아가는 알고리즘

- k번째 원소를 정렬한다고 하면 0에서 k - 1번째까지 원소들은 정렬된 상태이다.
- 안전 정렬에 속한다.

#### 시간 복잡도
- O(n^2)

#### 과정
- 배열 arr을 오름차순으로 정리한다고 가정한다.
- k(0 < k < arr_len)번째 index를 정렬한다고 하자.
- k번째 인덱스 값(이하 now_val)을 저장한다.
- arr의 m(k - 1 to 0)번째 index까지 값을 비교하며 now_val < arr\[m]이면 arr\[m + 1] = arr\[m]을 한다.
- 만일 now_val >= arr\[m]이면 m번째에 now_val을 넣고 k를 1 증가시킨다.