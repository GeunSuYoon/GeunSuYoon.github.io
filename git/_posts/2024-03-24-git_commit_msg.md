---
layout: post
categories:
  - git
title: 깃허브 커밋 메세지 변경
date: 2024-03-24 23:58:00 +09:00
tags:
---
>최근 유니티 공부를 하다 git push를 하는 과정에서 큰 용량 문제로 머리를 앓다 커밋 메시지를 'test'로 한 적이 있었다. 
>이를 변경하는 방법을 알아보자!

# git editor 변경

- 커밋 메시지를 변경하는 과정에서 터미널에서 편집하는 과정이 있다.
- 기본 편집기는 nano다.
- 비교적 익숙한 vim으로 바꿔주자!

	`$ git config --global core.editor "vim"`

- 해당 명령어를 입력하면 git 옵션으로 실행하는 파일 편집이 vim으로 바뀐다.

# git log 보기

	`$ git log`

- 해당 명령어를 입력하면 commit 이력을 볼 수 있고, 