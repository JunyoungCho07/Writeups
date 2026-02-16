find [경로] -user [사용자명] -group [그룹명] -size 33c -type f 2>/dev/null


find -size 33c -user bandit7 -group bandit6 2>/dev/null

/dev/null --> 쓰래기통

Permission denied --> stderr --> 쓰래기통에 버림


0 stdin
1 stdout
2 stderr