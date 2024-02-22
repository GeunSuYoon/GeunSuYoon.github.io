---
layout: post
categories:
  - boj
title: 이항 계수 3
date: 2024-02-22 16:23:00 +09:00
tags:
  - math
---

>[백준 11401. 이항 계수3]()의 풀이이다.


# 페르마의 소정리
- p가 소수이면, 모든 정수 a에 대해 a<sup>p</sup> ≅ a (mod p)
- p가 소수이고 a가 p의 배수가 아니면 a<sup>p-1</sup> ≅ 1 (mod p)

# 풀이
- <sub>n</sub>C<sub>k</sub> 는 n!/(k!(n-k)!)으로 표현할 수 있다.