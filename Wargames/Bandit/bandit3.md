Bandit Level 3 → Level 4
Level Goal
The password for the next level is stored in a hidden file in the inhere directory.

Commands you may need to solve this level
ls , cd , cat , file , du , find

Walkthrough
Step 1: 디렉터리 탐색 (Reconnaissance)
먼저 홈 디렉터리를 확인합니다.

bandit3@bandit:~$ ls -al
...
drwxr-xr-x 2 root root 4096 Oct 14 09:26 inhere
...
inhere라는 디렉터리가 존재함을 확인했습니다.

Step 2: 디렉터리 이동 및 숨겨진 파일 발견
"""
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$ ls -al
total 12
drwxr-xr-x 2 root    root    4096 Oct 14 09:26 .
drwxr-xr-x 3 root    root    4096 Oct 14 09:26 ..
-rw-r----- 1 bandit4 bandit3   33 Oct 14 09:26 ...Hiding-From-You
"""
...Hiding-From-You 파일이 발견되었습니다.

Step 3: 파일 내용 읽기
파일명이 점(.)으로 시작하므로, 안전하게 읽기 위해 **상대 경로(./)**를 명시하여 출력합니다.

bandit3@bandit:~/inhere$ cat ./...Hiding-From-You
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

3. Flag
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

learn
cd = change directory
.으로 시작하는 파일은 숨겨진 파일이며, ls -a 옵션으로 조회 가능하다.
. (점 하나): 현재 디렉터리 (Current Directory)

.. (점 둘): 상위 디렉터리 (Parent Directory)

... (점 셋): 아무런 특수 기능 없음. 그저 점으로 시작하는 일반 파일 이름일 뿐입니다.