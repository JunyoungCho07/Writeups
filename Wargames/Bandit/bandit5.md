find [경로] 
옵션
-size 1033c
-type f
! -executable

! = not




type??
ls -l 실행 시 가장 앞글자(drwxr-xr-x의 d)가 바로 이 -type과 일치합니다.

### `find` 명령어 `-type` 옵션 식별자 (File Type Descriptors)

| 식별자 (Descriptor) | 파일 형식 (File Type) | 설명 (Description) |
| :---: | :--- | :--- |
| **f** | **Regular File** | 일반 파일 (텍스트, 실행 파일, 이미지, 소스 코드 등) |
| **d** | **Directory** | 디렉토리 (폴더) |
| **l** | **Symbolic Link** | 심볼릭 링크 (다른 파일을 가리키는 바로가기) |
| **c** | **Character Special** | 캐릭터 장치 파일 (입출력이 한 번에 한 문자씩 일어나는 하드웨어) |
| **b** | **Block Special** | 블록 장치 파일 (데이터를 블록 단위로 읽고 쓰는 하드 드라이브 등) |
| **p** | **Named Pipe (FIFO)** | 프로세스 간 통신(IPC)을 위해 사용되는 파이프 파일 |
| **s** | **Socket** | 네트워크 통신 및 프로세스 간 로컬 통신을 위한 소켓 파일 |


1033c --> 1033byte
c는 **Character(Byte)**를 의미

find는 파일 시스템의 **Metadata(Inode)**에 기록된 st_size 값을 참조합니다.$n$: 정확히 $n$ 유닛.$+n$: $n$ 유닛 초과.$-n$: $n$ 유닛 미만.유닉스 시스템의 전통적인 블록 크기($512$ bytes)와 현대적인 바이트 단위 사이의 간극을 메우기 위해 접미사(c, k, M, G)가 도입되었습니다.

### `find` 명령어 `-size` 옵션 접미사 (Size Suffixes)

| 접미사 (Suffix) | 단위 (Unit) | 설명 (Description) |
| :---: | :--- | :--- |
| **b** | **512-byte blocks** | 기본 단위 (접미사를 생략할 경우 적용되는 Default 값) |
| **c** | **Bytes** | 정확한 바이트(Byte) 수 (Exact byte count) |
| **w** | **2-byte words** | 2바이트 워드(Word) 단위 |
| **k** | **Kibibytes** | 1,024 바이트 (KiB 단위) |
| **M** | **Mebibytes** | 1,048,576 바이트 ($1024^2$ B, MiB 단위) |
| **G** | **Gibibytes** | 1,073,741,824 바이트 ($1024^3$ B, GiB 단위) |