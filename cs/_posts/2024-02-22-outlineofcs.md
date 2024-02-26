---
layout: post
categories:
  - cs
  - os
title: 01. 컴퓨터 시스템 개요
date: 2024-02-22 19:06:00 +09:00
tags:
---

# Goal
- 컴퓨터 시스템의 기본 요소와 관계 이해
- 인터럽트 개념과 처리기의 인터럽트 사용 이유에 대한 이해
- 전형적인 컴퓨터 메모리 계층 구조 이해
- 멀티 프로세서의 기본 특성과 멀티 코어의 구조 이해

---

# 컴퓨터 구성 요소
1. 처리기(Central Processing Unit, CPU): 데이터 연산, 논리 연산(ALU), 제어(Control Unit), 레지스터(Register)
2. 주 기억 장치(Main Memory): 메모리 내의 개별적인 저장 공간 (휘발성)
3. 저장장치(Storage Device): 디스크, CD-ROM, 플로피 디스크, Flash Memory(비휘발성)
4. 입출력 장치
5. 통신 장치: Modem, Ethernet, Bluetooth

---

## 컴퓨터 구성 요소 (최상위 수준 관점)

![[Pasted image 20240226205151.png]]
- 메모리 주소 레지스터(Memory Address Register): 다음 번에 읽거나 쓸 주소 명시
- 메모리 버퍼 레지스터(Memory Buffer Register): 메모리에 쓸 데이터를 포함하거나 메모리로부터 수신된 데이터를 포함
- 프로그램 계수기(Program Counter): 다음 실행될 명령어의 주소(실행할 기계어 코드 위치)를 저장
- 명령어 레지스터(Instruction Register): 최근 반입된 명령어 포함(실행 중일 명령어)
- 누산기(AC): 연산 결과를 임시로 저장
- 프로그램 상태 워드(Program Status Word): 인터럽트 가능화/불능화

## 명령어 실행 2단계
![[Pasted image 20240226205446.png]]
