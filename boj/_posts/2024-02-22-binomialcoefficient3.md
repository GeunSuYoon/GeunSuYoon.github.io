---
layout: post
categories:
  - boj
title: 이항 계수 3
date: 2024-02-22 16:23:00 +09:00
tags:
  - math
---
# \[BOJ] 백준 이항 계수 3 11401

>[백준 11401. 이항 계수3]()의 풀이이다.

---

## 페르마의 소정리
- p가 소수이면, 모든 정수 a에 대해 a<sup>p</sup> ≅ a (mod p)
- p가 소수이고 a가 p의 배수가 아니면 a<sup>p-1</sup> ≅ 1 (mod p)

---

## 응용
- 정수 a, b, p에 대해 (p는 소수) 이하의 식으로 정리할 수 있다.
- b<sup>p-1</sup> = b\*b<sup>p-2</sup> ≅ 1 (mod p)
- b<sup>p-2</sup> ≅ b<sup>-1</sup> (mod p)
- a\ * b<sup>-1</sup> % p ≅ a\ * b<sup>p-2</sup>  % p (mod % p)

---

## 풀이
- p는 1,000,000,007로 주어졌다.
- <sub>n</sub>C<sub>k</sub> 는 a / b = a \* b<sup>-1</sup>로 표현할 수 있다. (a = n! / (n - k)!, b = k!)
- a \* b<sup>-1</sup> % p = a \* b<sup>p-2</sup> / b<sup>p-1</sup> % p≅ a \* b<sup>p-2</sup>  % p (mod p)
- a % p와 b<sup>p-2</sup>  % p를 따로 구해준 뒤 곱한 결과에 % p를 취한다.