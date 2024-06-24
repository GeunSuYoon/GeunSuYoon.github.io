---
layout: post
categories:
  - algorithm
title: "[Algorithm] Radix Sort"
date: 2024-02-21 19:19:00 +09:00
tags:
  - sort
---
# [Algorithm] 기수 정렬 (Radix Sort)

>Comparison Sort의 문제 해결.

## Radix Sort
- 데이터를 구성하는 기본 요소(Radix)를 이용하여 정렬.
- 입력 데이터의 최댓값에 따라 Counting Sort 대신 사용 가능.
	- 자릿수 기준이므로 나올 수 있는 최대 사이즈는 9(0~9).
## 시간복잡도
- O(d * (n + b)) > d는 자릿수, b는 10.

## 장단점
### 장점
- 문자열, 정수 정렬 가능.
### 단점
- 자릿수가 없는 것은 정렬 불가능(부동 소숫점 등)
- 중간 결과를 저장할 bucket 공간 필요.

## 구현 방법
- arrLen = arr.len;
- maxVal = max value of arr;
- for exp = 1 to exp of maxVal
	- bucketSort(arr, arrLen, exp);

### bucketSort(arr, arrLen, exp)
- bucket\[arrLen];
- count\[10];
- for cnt = 0 to arrLen - 1
	- count\[(arr\[cnt] / exp) % 10]++; //현재 자릿수에 맞춰 정렬
- for cnt = 1 to 9
	- count\[cnt] += count\[cnt - 1]; //누적합 계산
- for cnt = arrLen - 1 to 0 //counting sort
	- bucket\[count\[(arr\[cnt] / exp) % 10] - 1] = arr\[cnt];
	- count\[(arr / exp) % 10]--;
- for cnt = 0 to arrLen - 1
	- arr\[cnt] = bucket\[cnt];

## 왜 아래부터 측정하는가?
- MSD(Most Significant Digit)와 LSD(Least Significant Digit) 비교 문제
- MSD는 가장 큰 자릿수부터 counting sort
	- 마지막 자릿수까지 확인 필요 X.
	- 정렬 됐는지 확인하는 과정이 필요해 추가적인 메모리 사용.
	- 알고리즘이 일관되지 않음 (만일 exp가 다른 값들이 있다면 따로 sorting해줘야 함.)
- LSD는 가장 작은 자릿수부터 counting sort
	- 마지막 자릿수까지 확인해야 함.
	- 중간에 정렬 결과를 알 수 없음.
	- 알고리즘이 일관됨.
	- LSD의 경우 자릿수가 정해진 경우 좀 더 빠를 수 있음.
