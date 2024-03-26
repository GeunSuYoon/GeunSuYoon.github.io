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
- 하지만, 익숙하지 않은 작업에 commit massage를 test로 여러 번 시도하던 중 commit이 성공했다!!
- 그러고 다른 작업을 하던 중 commit massage가 test로 남아있는 모습을 보게 됐다.
	- 물론, 다른 작업을 push하기 전에 가장 최근 massage만 바꾸려면 `$ git commit --amend -m "NEW MASSAGE"` 로 바꾸면 된다!
- 이번엔 이것을 바꾸는 방법을 알아보자!
# git editor 변경

- 커밋 메시지를 변경하는 과정에서 터미널에서 편집하는 과정이 있다.
- 기본 편집기는 nano다.
- 비교적 익숙한 vim으로 바꿔주자!

	`$ git config --global core.editor "vim"`

- 해당 명령어를 입력하면 git 옵션으로 실행하는 파일 편집이 vim으로 바뀐다.

# git log 보기

- 다른 일을 할 때도 git log를 봐야 하는 경우가 있다.

	`$ git log`

- 해당 명령어를 입력하면 해당 repository의 기록을 볼 수 있다.

![git_log](public/img/_src/git/commit_msg_change/02.git_log.png)

- 파란 선이 내가 test로 commit massage를 보낸 hash key이다.
- 하지만, rebase로 해당 로그로 이동하면 그 다음 기록부터 보인다.
	- feat: Destroy enemy when hitten by bullet 부터 보인다는 뜻이다.
- 그래서 우린 빨간 선, 즉 이전 기록인 docs: Create README.md file의 hash key를 복사하자.

# git rebase

- 이제 우리는 변경을 할 수 있는 위치를 알았다. 그렇다면 이제 이동해보자!

	`$ git rebase -i [HASH_KEY]`

- 위 명령어를 입력하면 앞서 말한 것처럼 다음 기록부터 보인다. 

![git_rebase_hash](public/img/_src/git/commit_msg_change/03.git_rebase_hash.png)

- 각 commit massage 앞에 `pick` 이라고 적힌 것을 볼 수 있다. 해당 명령어는 아래 파란 글씨로 적힌 `Commands:` 아래 적힌 의미이다.
- 우린 test의 커맨드를 `pick`에서 `reword`로 바꿀 것이다.

![git_rebase_target_cmd_change](public/img/_src/git/commit_msg_change/04.git_rebase_target_cmd_change.png)



![](public/img/_src/git/commit_msg_change/05.change_commit_msg.png)

![](public/img/_src/git/commit_msg_change/06.after_msg_change_terminal.png)

![](public/img/_src/git/commit_msg_change/07.git_push_option_to_change_github.png)

![](public/img/_src/git/commit_msg_change/07_1.git_push_option_with_no_includes.png)

![](public/img/_src/git/commit_msg_change/08.after_change_msg.png)


# git log 보기

	`$ git log`

- 해당 명령어를 입력하면 commit 이력을 볼 수 있고, 