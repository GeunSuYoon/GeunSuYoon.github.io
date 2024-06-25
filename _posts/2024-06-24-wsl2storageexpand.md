---
layout: post
categories:
  - etc
title: "[ETC] WSL2 용량 확보"
date: 2024-06-24 19:10:00 +09:00
tags:
---
# [ETC] WSL2 용량 확보

- 최근 wsl2를 사용하던 중 용량이 가득 차버렸다.
	- 학교 과제 데이터를 압축 해제하는데 용량을 확인하지 않았다 ㅠㅠ
- 문제는 이후 wsl2가 제대로 연결되지 않았다!
- 그래서 해당 문제를 해결한 방법을 소개하려 한다!

## 용량 추가

- 해당 방법은 Windows Powershell을 관리자 권한으로 열어 진행해야 한다.
	- 난 cmd로 열어서 했는데 중간부터 안돼 많이 당황했다...

### 1. wsl 종료

- Windows PowerShell을 관리자 권한으로 실행해 아래 명령어를 입력한다.
	- `wsl.exe --shutdown`
- 해당 명령어로 모든 wsl instance를 종료해 예기치 못한 오류를 방지한다.
### 2. wsl 경로 확인

- C:\\Users\\{{ user_name }}\\AppData\\Local\\Packages
- 보통 위 경로에서 본인이 관리하고 싶은 배포판을 확인해 들어간다.
	- 나의 경우 CanonicalGroupLimited.Ubuntu20.04LTS_79 였다.
- 배포판 폴더 내부 LocalState 폴더에 들어가면 ext4.vhdx 파일이 있다.
	- 해당 파일이 가상 하드디스크이다!
### 3. diskpart

- PowerShell에 `diskpart` 명령어를 입력한다.
	- DISKPART> 가 나온다면 성공이다!
- `Select vdisk file="<pathToVHD>"` 명령어로 가상 디스크 파일을 선택한다.
	- \\<pathToVHD\>는 2번에서 확인한 ext4.vhdx 파일을 포함한 경로다!!!
- `detail vdisk`를 실행해 가상 디스크의 정보를 확인한다.
	- cmd로 실행하면 아래와 같이 나온다.
	- ![[cmd_detail_vdisk.png]]
	- 장치 유형도 확인할 수 없고, 공급업체 ID도 알 수 없다.
	- 마지막 줄을 확인해보니 연결된 디스크가 없다...
	- 그러면 이후 동작이 실행되지 않는다!!!!
- `expand vdisk maximum=<sizeInMegaBytes>` 명령어로 가상 디스크에 할당하는 크기를 늘리자!
	- \\<sizeInMegaBytes\>는 바꿀 크기를 MB 단위로 입력하란 뜻이다.
	- 난 20GB를 할당할 것이므로 20000을 입력했다!
	- cmd로 실행하면 아래와 같이 나온다.
	- ![[cmd_expand_vdisk.png]]
- 이제 `exit` 명령어로 diskpart를 종료하고 wsl을 켜면 동작할 것이다!!!!!!!
- 아래와 같이 진행돼야 한다.
- ![[powershell_diskpart.png]]

## 여담

- cmd와 powershell을 잘 구분했다면 30분은 일찍 끝낼 수 있었을 것이다.
	- 안타까우신거지...
- 앞으로는 가용 용량과 파일 용량을 제대로 확인하는 습관을 들여야겠다.
- 용량 추가 외에 압축하는 방법도 있다고 하는데 다음에 해보면 좋을 것 같다!!