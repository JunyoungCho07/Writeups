find [경로] -user [사용자명] -group [그룹명] -size 33c -type f 2>/dev/null


find -size 33c -user bandit7 -group bandit6 2>/dev/null

/dev/null --> 쓰래기통

Permission denied --> stderr --> 쓰래기통에 버림


0 stdin
1 stdout
2 stderr

shutdown -h now

명령어 실행 시 내부적으로 다음과 같은 State Transition이 발생합니다:

Broadcast: 모든 로그인된 사용자에게 시스템 종료 예고 메시지를 보냅니다.

Inhibition: 새로운 사용자의 로그인을 차단합니다.

SIGTERM & SIGKILL: init(또는 systemd) 프로세스가 실행 중인 모든 프로세스에 SIGTERM을 보내 안전한 종료를 유도하고, 응답이 없으면 SIGKILL로 강제 종료합니다.

Sync: 파일 시스템의 버퍼를 디스크로 강제로 옮깁니다 (sync).

Halt/Poweroff: 커널을 중단시키고 메인보드에 전원 차단 신호를 보냅니다.


### 1. `shutdown` 명령어 옵션 (State Options)

| 옵션 (Option) | 기능 (Function) | 상세 설명 (Detailed Description) |
| :---: | :--- | :--- |
| **`-h`** | **Halt / Power-off** | 시스템을 정지하거나 전원을 차단함 (가장 보편적 사용) |
| **`-P`** | **Power-off** | 하드웨어 전원을 완전히 끔 (ACPI S5 상태 진입) |
| **`-H`** | **Halt** | 운영체제 커널은 중지시키되, 하드웨어 전원은 유지할 수 있음 |
| **`-r`** | **Reboot** | 시스템 종료 후 즉시 재부팅 (시스템 업데이트 후 필수) |
| **`-k`** | **Kidding (Warn)** | **실제로 끄지 않음.** 접속자들에게 경고 메시지만 전송 (테스트용) |
| **`-c`** | **Cancel** | 이미 예약된(Time이 설정된) 종료 명령을 즉시 취소함 |

---

### 2. 시간 지정 인자 (Time Arguments)

| 형식 (Format) | 예시 (Example) | 설명 (Description) |
| :---: | :--- | :--- |
| **`now`** | `shutdown -h now` | 지연 시간 없이 즉시 시스템 종료 실행 |
| **`+m`** | `shutdown -r +15` | 현재 시점으로부터 `m`분 후에 실행 (예: 15분 후 재부팅) |
| **`hh:mm`** | `shutdown -h 23:30` | 24시간 형식의 특정 시각에 실행 예약 |

---

### 3. 메시지 인자 (Wall Message)

| 구성 (Structure) | 예시 (Example) | 설명 (Description) |
| :--- | :--- | :--- |
| **`[MESSAGE]`** | `"System Upgrade"` | 모든 로그인 사용자 터미널에 전달될 커스텀 경고 문구 |

---

### 4. 종합 활용 예시 (Composite Examples)

* **10분 뒤 커스텀 메시지와 함께 종료:**
    `shutdown -h +10 "서버 점검 예정입니다. 작업을 저장하세요."`
* **새벽 2시에 재부팅 예약:**
    `shutdown -r 02:00 "Scheduled Weekly Reboot"`
* **예약된 종료 취소:**
    `shutdown -c`