# [Bandit] Level X → Level Y

## 1. 목표 (Objective)
- 이름이 -인 파일 읽기

## 2. 사용 명령어 (Commands)
- `ls`, `cat`

## 3. 해결 과정 (Walkthrough)
1. **환경 분석**: 홈 디렉토리에 무엇이 있는지 `ls -al`로 확인.
2. **파일 탐색**: `-` 파일이 있음을 확인.
3. **실패**: `cat -` 명령어로 읽기 실패.
4. **실패**: `cat \-` 명령어로 읽기 실패.
5. **실패**: `cat "-"` 명령어로 읽기 실패.
6. **성공**: `cat ./-` 상대위치로 명시하여 파일 읽기 성공.
   - *결과값 (Output)*: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

## 4. 최종 비밀번호 (Flag)
- `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`

## 5. 학습 내용 (Learnings)
- **상대경로와 절대경로**: ./ --> 지금 위치, ../ --> 상위 폴더, /~~~~~~ 절대경로