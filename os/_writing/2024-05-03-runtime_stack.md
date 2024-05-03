---
layout: post
categories:
  - os
title: "[Lecture - OS] 03. Runtime Stack"
date: 2024-05-03 17:08:00 +09:00
tags:
---
# \[Lecture - OS] Runtime stack

>우리가 작성한 코드를 실제 실행할 때 컴퓨터는 stack을 이용해 함수의 흐름을 제어한다.

## C Program Naming

- Function
- Variable
	- Global Variable (static)
	- Local Variable (dynamic)
- Heap
	- Dynamic memory object

## Compile

- 위에서 언급한 naming은 compile 할 때 address로 바뀐다.
- Compiler는 모든 address value(Logical address)를 알고 있다.
	- Global variable은 space address에 logical address로 할당된다.
	- 다만, local variable은 주소를 할당 받지 않아 모른다.
	- 이것을 stack에 register 저장해 활용한다!

## Assembly Code

- 
### H3 tag (element about H2 tag)
- explane about H3 tag