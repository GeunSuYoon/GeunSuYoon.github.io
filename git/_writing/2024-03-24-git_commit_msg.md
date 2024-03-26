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

![before_change_msg](public/img/_src/git/commit_msg_change/01.before_change_msg.png)
- 최근 unity 공부를 하던 중, 기존 unity 프로젝트 폴더 내부 파일을 만든 repository에 추가하려 했다.
- pull request에 익숙해지려 PR을 하는 방식으로 여러 번 push했다.
- 하지만, 익숙하지 않은 작업에 제대로 동작하지 않아 commit massage를 test로 여러 번 시도하던 중 commit
# git editor 변경

- 커밋 메시지를 변경하는 과정에서 터미널에서 편집하는 과정이 있다.
- 기본 편집기는 nano다.
- 비교적 익숙한 vim으로 바꿔주자!

	`$ git config --global core.editor "vim"`

- 해당 명령어를 입력하면 git 옵션으로 실행하는 파일 편집이 vim으로 바뀐다.

![](public/img/_src/git/commit_msg_change/02.git_log.png)

![](public/img/_src/git/commit_msg_change/03.git_rebase_hash.png)

![](public/img/_src/git/commit_msg_change/04.git_rebase_target_cmd_change.png)

![](public/img/_src/git/commit_msg_change/05.change_commit_msg.png)

![](public/img/_src/git/commit_msg_change/06.after_msg_change_terminal.png)

![](public/img/_src/git/commit_msg_change/07.git_push_option_to_change_github.png)

![](public/img/_src/git/commit_msg_change/07_1.git_push_option_with_no_includes.png)

![](public/img/_src/git/commit_msg_change/08.after_change_msg.png)


# git log 보기

	`$ git log`

- 해당 명령어를 입력하면 commit 이력을 볼 수 있고, 