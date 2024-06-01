---
layout: post
categories:
  - git
title: "[GIT] 깃허브 커밋 메세지 변경"
date: 2024-03-24 23:58:00 +09:00
tags:
---
# \[GIT] 깃 커밋 메세지 변경

>최근 유니티 공부를 하다 git push를 하는 과정에서 큰 용량 문제로 머리를 앓다 커밋 메시지를 'test'로 한 적이 있었다. 
>이를 변경하는 방법을 알아보자!

![before_change_msg](/public/img/git_commit_msg_change_01.before_change_msg.png)

- 최근 unity 공부를 하던 중, 기존 unity 프로젝트 폴더 내부 파일을 만든 repository에 추가하려 했다.
- pull request에 익숙해지려 PR을 하는 방식으로 여러 번 push했다.
- 하지만, 익숙하지 않은 작업에 commit massage를 test로 여러 번 시도하던 중 commit이 성공했다!!
- 그러고 다른 작업을 하던 중 commit massage가 test로 남아있는 모습을 보게 됐다.
	- 물론, 다른 작업을 push하기 전에 가장 최근 massage만 바꾸려면 `$ git commit --amend -m "NEW MASSAGE"` 로 바꾸면 된다!
- 이번엔 이것을 바꾸는 방법을 알아보자!
## git editor 변경

- 커밋 메시지를 변경하는 과정에서 터미널에서 편집하는 과정이 있다.
- 기본 편집기는 nano다.
- 비교적 익숙한 vim으로 바꿔주자!

	`$ git config --global core.editor "vim"`

- 해당 명령어를 입력하면 git 옵션으로 실행하는 파일 편집이 vim으로 바뀐다.

## git log 보기

- 다른 일을 할 때도 git log를 봐야 하는 경우가 있다.

	`$ git log`

- 해당 명령어를 입력하면 해당 repository의 기록을 볼 수 있다.

![git_log](/public/img/git_commit_msg_change_02.git_log.png)

- 파란 선이 내가 test로 commit massage를 보낸 hash key이다.
- 하지만, rebase로 해당 로그로 이동하면 그 다음 기록부터 보인다.
	- feat: Destroy enemy when hitten by bullet 부터 보인다는 뜻이다.
- 그래서 우린 빨간 선, 즉 이전 기록인 docs: Create README.md file의 hash key를 복사하자.

## commit massage 바꾸기

- 이제 우리는 변경을 할 수 있는 위치를 알았다. 그렇다면 이제 이동해보자!
- 이동하는 것은 rebase로 할 수 있다.

	`$ git rebase -i [HASH_KEY]`

- 위 명령어를 입력하면 앞서 말한 것처럼 다음 기록부터 보인다. 

![git_rebase_hash](/public/img/git_commit_msg_change_03.git_rebase_hash.png)

- 각 commit massage 앞에 `pick` 이라고 적힌 것을 볼 수 있다. 해당 명령어는 아래 파란 글씨로 적힌 `Commands:` 아래 적힌 의미이다.
- 우린 test의 커맨드를 `pick`에서 `reword`로 바꿀 것이다.

![git_rebase_target_cmd_change](/public/img/git_commit_msg_change_04.git_rebase_target_cmd_change.png)

- 이제 우리는 해당 commit massage를 바꾸겠다고 선언했다. 해당 파일을 저장하고 종료하면 아래와 같은 화면이 나온다.

![change_commit_msg](/public/img/git_commit_msg_change_05.change_commit_msg.png)

- 이미 변경한 사진이지만, 원래는 기존 massage인 test가 들어가 있다.
- 바꾸고 저장하고 나오자.

![after_msg_change_terminal](/public/img/git_commit_msg_change_06.after_msg_change_terminal.png)

- 그럼 위와 같이 massage가 update됐다는 안내가 나온다.

## 수정 사항 git push하기

- 그럼 이제 push를 해주자. 그런데 그냥 git push를 하면 안 올라간다.
- 그 이유는 크게 두 가지가 있다.
	1. Hash 값 변경
	2. 원격 저장소와 로컬 저장소 충돌
- 이럴 때 우리는 강제로 push해야 한다.
- 강제로 push하는 명령어는 아래와 같다.

	`$ git push --force`

- 하지만, 해당 명령어는 말 그대로 강제로 밀어 넣기 때문에 협업 환경에서 다른 사람들의 결과물을 망칠 수 있다.
- 그러므로 force 뒤에 추가 옵션을 준다.

	`$ git push --force-with-lease`

- 위 옵션은 로컬과 원격 저장소의 동기화 상태를 확인한다.
- 만일 원격 저장소에 변경 사항이 있다면 실패해 충돌을 방지한다!

![git_push_option_with_no_includes](/public/img/git_commit_msg_change_07_1.git_push_option_with_no_includes.png)

## 결과

![after_change_msg](/public/img/git_commit_msg_change_08.after_change_msg.png)

- 그럼 우린 원격 저장소의 commit massage가 바뀐 것을 확인할 수 있다!!