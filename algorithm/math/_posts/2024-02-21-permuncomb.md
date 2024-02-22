---
layout: post
categories:
  - algorithm
title: Permutation & Combination
date: 2024-02-21 19:10:00 +09:00
tags:
  - math
---
# Permutation & Combination

>순열과 조합. 아래에 나오는 n은 전체 집합 요소의 개수, r은 해당 부분 집합의 길이를 의미한다.


### Permutation (순열, nPr)
- 순서를 정해서 부분 집합을 만드는 방법.
- 즉, 같은 요소들로 차있더라도 순서가 다르다면 다른 것으로 인식한다.
- 총 부분 집합의 개수는 아래와 같이 계산할 수 있다.
>nPr = n * (n - 1) * (n - 2) * ... * (n - r + 1)

#### 중복 순열
- 요소의 중복을 허용하는 순열.
- 총 부분 집합의 개수는 n^r개다.

### Combination (조합, nCr)
- 순서 없이 부분 집합을 만드는 방법.
- 같은 요소들로 차 있다면 같은 것으로 인식한다.
- 총 부분 집합의 개수는 아래와 같이 계산할 수 있다.
	- <sub>n</sub>C<sub>r</sub> = n * (n - 1) * (n - 2) * ... * (n - r + 1) / r!
- nCr은 두 조합의 합으로 나눌 수 있다.
	- <sub>n</sub>C<sub>r</sub> = <sub>n-1</sub>C<sub>r</sub> + <sub>n-1</sub>C<sub>r - 1</sub>

#### 중복 조합
- 요소의 중복을 허용하는 조합.
- 총 부분 집합의 개수는 <sub>n</sub>H<sub>r</sub> = <sub>n+r-1</sub>C<sub>r</sub> = <sub>n+r-1</sub>C<sub>n-1</sub>