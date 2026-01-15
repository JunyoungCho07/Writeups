Level Goal
The password for the next level is stored in a file called --spaces in this filename-- located in the home directory

Commands you may need to solve this level
ls , cd , cat , file , du , find

Walkthrough
`ls -al`
`cat ./--` tab 클릭 --> `cat ./--spaces\ in\ this\ filename--` 자동완성

Final output
bandit2@bandit:~$ cat ./--spaces\ in\ this\ filename-- 
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

Flag
`MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`

Learnings
스페이스는 이스케이프 코드를 써야하는구나
자동완성을 잘 쓰자.
근데 왜 앞 문제 `cat \-`는 안 먹혔지? 상대위치 내에서 이스케이프문제가 먹히는건가???

핵심 질문: 왜 cat \-는 실패하고, cat spaces\ ...는 성공했는가?
이전 레벨의 - 파일과 이번 레벨의 공백 파일은 **실패의 원인이 발생하는 층위(Layer)**가 서로 다릅니다.

1) 공백(Space)의 경우: 범인은 '쉘(Shell)'
현상: cat spaces in this filename이라고 입력하면 쉘은 이것을 cat, spaces, in, this, filename이라는 5개의 명령/인자로 쪼개버립니다.

해결: 역슬래시(\)를 붙여 spaces\ in...으로 만들면, 쉘에게 **"이 공백은 쪼개는 기준이 아니라 이름의 일부야"**라고 알려주게 됩니다.

결과: 쉘이 파일명을 온전하게 cat에게 전달합니다.

2) 대시(-)의 경우: 범인은 '프로그램(Cat)'
현상: cat -를 입력하든 cat \-를 입력하든, 쉘은 대시 문자(-)를 cat 프로그램에게 아주 잘 전달했습니다. (쉘은 -를 쪼개는 기준으로 쓰지 않으니까요.)

문제: 전달받은 cat 프로그램 내부의 **정의(Definition)**가 문제입니다. 리눅스 표준에서 -는 파일 이름이 아니라 **표준 입력(STDIN)**을 의미하기 때문입니다.

`그럼 쉘의 문법적으로 -가 문제되는 경우는 없는가?`

아주 날카로운 질문입니다. "네, 있습니다."

일반적인 상황(파일명 등)에서 -는 그냥 문자로 취급되지만, 쉘의 문법(Shell Grammar) 자체에서 -를 **특수 기능(Operator)**으로 해석하는 경우가 분명히 존재합니다.

단순히 "프로그램의 옵션"으로 오해받는 것을 넘어, 쉘(bash/zsh)이라는 언어 자체가 -를 문법적으로 처리하는 3가지 핵심 케이스를 정리해 드립니다.

1. 와일드카드 범위 지정 (Globbing Range)
쉘이 *나 ? 같은 패턴을 해석할 때, 대괄호 [] 안에서의 -는 문자가 아니라 **"범위(Range)"**라는 문법적 의미를 갖습니다.

문법: [시작문자-끝문자]

2. 산술 연산자 (Arithmetic Operator)
쉘 내부에서 수학 계산을 하는 문법인 $(( ... )) 안에서 -는 **"뺄셈 기호"**입니다.

문법: $(( 숫자 - 숫자 ))

3. 변수 기본값 처리 (Parameter Expansion)
쉘 스크립트에서 변수가 비어있을 때 "기본값"을 지정하는 문법에 -가 사용됩니다.

문법: ${변수명:-기본값}