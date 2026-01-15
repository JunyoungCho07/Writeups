Bandit Level 4 → Level 5
Level Goal
The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

Commands you may need to solve this level
ls , cd , cat , file , du , find

2. Walkthrough (Solution)

Step 1: 디렉터리 진입 및 탐색

inhere 디렉터리로 이동하여 파일 목록을 확인합니다.

bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$ ls -al
total 48
drwxr-xr-x 2 root    root    4096 Oct 14 09:26 .
drwxr-xr-x 3 root    root    4096 Oct 14 09:26 ..
-rw-r----- 1 bandit5 bandit4   33 Oct 14 09:26 -file00
# ... (-file09 까지 존재) ...


-file00부터 -file09까지 이름이 유사한 10개의 파일이 존재합니다. 파일명만으로는 어떤 파일이 정답인지 알 수 없습니다.

Step 2: 내용 확인 (Brute Force)

파일의 내용을 하나씩 출력하여 사람이 읽을 수 있는 텍스트인지 확인합니다.
이때, 파일명이 대시(-)로 시작하므로 **상대 경로(./)**를 사용하여 cat 명령어를 실행합니다.

bandit4@bandit:~/inhere$ cat ./-file00
=I V`n5ѳ*G^7cO  # (Binary Data - 깨진 문자)

bandit4@bandit:~/inhere$ cat ./-file01
0w8qYdZCF+ # (Binary Data - 깨진 문자)

# ... (중략) ...

bandit4@bandit:~/inhere$ cat ./-file07
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw # (Human-readable Text 발견!)


대부분의 파일이 바이너리 데이터로 인해 깨진 문자를 출력했으나, -file07에서 명확한 ASCII 문자열을 발견했습니다.

단순 반복으로 찾았지만, find명령어를 사용하면 더 간단한 방법ㅇ 있을거라 생각하여, 저렇게 푼 후 find명령어 풀이를 찾아봤습니다.

3. Flag
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

4. Learnings & Deep Dive

이번 풀이에서는 하나씩 열어보는 방식을 사용했지만, 파일이 많을 경우를 대비해 **데이터의 타입(Type)**을 먼저 식별하는 것이 효율적입니다.

컴퓨터 파일은 크게 두 가지로 나뉩니다.

- 바이너리 파일 (Binary): 컴퓨터가 이해하는 0과 1의 데이터 (실행 파일, 이미지 등). cat으로 열면 터미널에서 깨진 문자가 출력됩니다.

- 텍스트 파일 (Text/ASCII): 사람이 읽을 수 있는 문자 코드로 구성된 데이터. Human-readable하다는 것은 바로 이 텍스트 파일을 의미합니다.

도구 (Tool): file 명령어

file 명령어는 파일의 **이름(Name)**이나 **확장자(Extension)**를 신뢰하지 않고, 파일 헤더(Header)에 숨겨진 고유 서명인 **매직 넘버(Magic Number)**를 판독하여 데이터의 **실체(True Type)**를 식별하는 명령어입니다.

핵심 근거: 리눅스 커널은 확장자(.txt, .jpg)를 기능적으로 무시합니다. 파일이 '무엇'인지는 오직 그 내용(Content)이 결정합니다.

정석 풀이법:

bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: OpenPGP Public Key
./-file02: OpenPGP Public Key
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text <---정답
./-file08: data
./-file09: data


*가 무엇인가?
1. 정의 (Definition)
*는 쉘의 글로빙(Globbing) 기능에서 사용되는 **와일드카드(Wildcard)**로, **"0개 이상의 모든 문자열"**과 매칭된다는 의미를 가집니다.

Globbing: 쉘이 파일 이름 패턴을 실제 파일 이름 목록으로 확장(Expansion)하는 과정.

Wildcard: 카드 게임의 '조커'처럼 무엇이든 될 수 있는 문자.

*는 shell이 처리함

Before Expansion: file ./*

During Expansion (Shell): file ./file00 ./file01 ./file02 ... ./file09

After Expansion (Process): file 명령어 프로세스는 10개의 인자(Argument)를 받게 됨.

다양한 패턴 예시:

*.txt: 확장자가 .txt인 모든 파일.

file*: 이름이 file로 시작하는 모든 파일.

*pass*: 이름 중간에 pass가 들어가는 모든 파일.

