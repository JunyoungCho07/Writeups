# [Bandit] Level 0 → Level 1

## 1. 목표 (Objective)
- readme 파일에서 비밀번호 찾기

## 2. 사용 명령어 (Commands)
- `ls`, `cat`, `file`, `ssh`

## 3. 해결 과정 (Walkthrough)
0. **서버 접속**: 'ssh bandit0@bandit.labs.overthewire.org -p 2220'를 이용해 bandit0계정으로 접속
1. **환경 분석**: 홈 디렉토리에 무엇이 있는지 `ls -al`로 확인.
2. **파일 탐색**: `readme` 파일이 있음을 확인.
3. **내용 출력**: `cat readme` 명령어로 내용 확인.
   - *결과값 (Output)*:
bandit0@bandit:~$ cat readme
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

## 4. 최종 비밀번호 (Flag)
- `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

## 5. 학습 내용 (Learnings)
- **명령어 옵션**: `ls -a`는 숨김 파일을 보여준다.
- **SSH의 명령 구조**: `ssh [계정]@[시스템주소] -p [포트번호]`
- **개념**: 리눅스에서 점(.)으로 시작하는 파일은 숨김 파일이다.
- a = all
- l = long listing
