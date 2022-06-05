#### 컴퓨터공학과_20213084_노승우


## 리눅스 명령어 : top, ps, jobs, kill 명령어 조사하기

###  1. top 명령어
top 명령어는 현재 OS의 상태를 나타내주는 CLI 어플리케이션이다.

메모리 사용량, CPU 사용량 등을 나타내주며 top를 실행하는 동안에는 주기적인 업데이트로 실시간에 근접한 내용을 보여준다.
 
![1](https://user-images.githubusercontent.com/60350405/172050960-2e7f4272-085d-42e8-ae53-d432562d5ab6.png)

#### * 요약영역
전체 프로세스가 OS에 대해서 리소스를 어느정도 차지하고 있는지를 알려준다.
 
 대표적인 값으로는 시간, 유저, 로드 에버리지(Load Average), 테스크(Tasks), CPU, 메모리(memory)가 있다.
 
 * 시간
 
> 가장 먼저 보이는 것이 현재 시간
> 
> 다음으로 표시되는 것이 OS가 살아있는 시간
> 
> 그리고 다음 나타나는것이 현재 접속중인 유저 세션 수
 
 * 로드 애버리지(Load Average)
 
> CPU Load의 이동 평균를 표시
> 
 * 테스크(Tasks)
 
> 현재 프로세스들의 상태를 나태내주는 영역
> 
> Total은 전체 프로세스
>  
> running은 running 상태인 프로세스의 수
> 
> sleeping은 대기상태인 프로세스의 수
> 
> stopped는 종료된 프로세스의 수
> 
> zombies는 좀비상태인 프로세스의 수
> 
 * CPU 사용량
 
> us : 프로세스의 유저 영역에서의 CPU 사용률
>
> sy : 프로세스의 커널 영역에서의 CPU 사용률
> 
> ni : 프로세스의 우선순위(priority) 설정에 사용하는 CPU 사용률
> 
> id : 사용하고 있지 않는 비율
> 
> wa : IO가 완료될때까지 기다리고 있는 CPU 비율
> 
> hi : 하드웨어 인터럽트에 사용되는 CPU 사용률
> 
> si : 소프트웨어 인터럽트에 사용되는 CPU 사용률
> 
> st : CPU를 VM에서 사용하여 대기하는 CPU 비율
>
 * 메모리(memory) 사용량 
 
> Mem : RAM의 메모리 영역
> 
> Swap : 디스크를 메모리 처럼 이용
> 
> 
> |total|총 메모리 양|
> |------|------------------| 
> |free|사용가능한 메모리 양|
> |used|사용중인 메모리 양|


#### 디테일 영역
![2](https://user-images.githubusercontent.com/60350405/172051790-b7a316bc-fdf2-41f0-a047-a6a4b5b43252.png)

* PID
 
> PID는 프로세스 ID이며 프로세스를 구분하기 위한 겹치지않는 고유한 값입니다.
 * USER
> 해당 프로세스를 실행한 USER 이름 또는 효과를 받는 USER의 이름입니다.
 * PR & NI
> PR : 커널에 의해서 스케줄링되는 우선순위입니다.
> NI : PR에 영향을 주는 nice라는 값입니다.

 * VIRT, RES, SHR, %MEM
> |이름|설명|
> |-----|:-------------------------------------------------------------:|
> |VIRT|프로세스가 소비하고 있는 총 메모리입니다. 프로그램이 실행중인 코드, heap, stack과 같은 메모리, IO buffer 메모리를 포함합니다.|
> RES|RAM에서 사용중인 메모리의 크기를 나타냅니다.|
> |SHR|다른 프로세스와의 공유메모리(Shared Memory)를 나타냅니다.|
> |%MEM|RAM에서 RES가 차지하는 비율을 나타냅니다.|
 S : 프로세스의 현재 상태를 나타냅니다.
 
 TIME+ : 프로세스가 사용한 토탈 CPU 시간
 
 COMMAND : 해당 프로세스를 실행한 커맨드를 나타냅니다.

#### 유명한 top용 커맨드
|명령어|설명|
|:----:|:------------------------------------------:|
|k| 프로세스를 모니터링하며 프로세스를 종료|
|M|메모리 사용량을 기준으로 정렬|
|P|CPU 사용량을 기준으로 정렬|
|N|프로세스 ID 기준으로 정렬|
|T|러닝타임 기준으로 정렬|
|R|오름차순과 내림차순을 토글 변경|
|H|쓰레드(thread)를 기본으로하여 정보를 보여 줌|
|o,O|필터링(COMMAND,%CPU 등등)|



---

### 2. ps 명령어
현재 실행중인 프로세스 목록과 상태를 보여준다.

원하는 프로세스의 상태를 출력하기 위해선 정확한 옵션 사용이 중요

* ps 사용법

> ```vim
>  $ ps [option]
>  ```

* ps 옵션

|옵션|설명|
|:------:|:------------------------------------------:|
|-A|모든 프로세스를 출력|
|a|터미널과 연관된 프로세스를 출력|
|-a|세션 리더를 제외하고 터미널에 종속되지 않은 모든 프로세스를 출력|
|-e|커널 프로세스를 제외한 모든 프로세스를 출력|
|-f|풀 포맷으로 보여줌. 유닉스 스타일로 출력해주는 옵션으로 UID, PID, PPID등이 함께 표시됨|
|-l, l|긴 포맷으로 보여줌. 프로세스의 정보를 길게 보여주는 옵션으로 PRI, NI값을 표시|
|-o 값|출력 포맷을 지정하는 옵션으로 값으로는 pid, tty, time, cmd 등을 지정|
|-M|64비트 프로세스들을 보여줌|
|-m|프로세스들 뿐만 아니라 커널 스레드들도 보여줌|
|-p|특정 PID를 지정할 때 사용|
|-r|현재 실행 중인 프로세서를 보여줌|
|u|프로세스의 소유자를 기준으로 출력|
|-u|특정 사용자의 프로세스 정보를 확인할 때 사용|
|x|터미널에 종속되지 않는 프로세스를 출력|
|-x|로그인 상태에 있는 동안 아직 완료되지 않은 프로세서들을 보여줌|

* ps 항목

|항목|설명|
|:----:|:------------------------------------------:|
|USER|BSD계열에서 나타나는 항목으로 프로세스 소유자의 이름|
|UID|SYSTEM V계열에서 나타나는 항목으로 프로세스 소유자의 이름|
|PID|프로세스의 식별번호|
|PPID|부모 프로세스 ID|
|%CPU|CPU 사용 비율의 추정치|
|%MEM|메모리의 사용 비율의 추정치|
|VSZ|K단위 또는 페이지 단위의 가상메모리 사용량|
|RSS|실제 메모리 사용량|
|TTY|프로세스와 연결된 터미널|
|S, STAT|현재 프로세스의 상태 코드|
|TIME|총 CPU 사용 시간|
|COMMAND|프로세스의 실행 명령행|
|STIME|프로세스가 시작된 시간 혹은 날짜|
|C, CP|짧은 기간 동안의 CPU 사용률|
|F|프로세스의 플래그|
|PRI|실제 실행 우선순위|
|NI|nice 우선순위 번호|


---

### 3. jobs 명령어

현재 쉘 프로세스의 지식 백그라운드 프로세스들을 표시

* jobs 상태

|상태|설명|
|:---------:|:------------------------------------------:|
|Running|작업이 계속 진행중임|
|Done|작업이 완료되어 0을 반환|
|Donecode|작업이 종료되었으며 0이 아닌 코드를 반환|
|Stopped|작업이 일시 중단|
|Stopped(SIGTSTP)|SIGTSTP 시그널이 작업을 일시 중단|
|Stopped(SIGSTOP)|SIGSTOP 시그널이 작업을 일시 중단|
|Stopped(SIGTTIN)|SIGTTIN 시그널이 작업을 일시 중단|
|Stopped(SIGTTOU)|SIGTTOU 시그널이 작업을 일시 중단|

* jobs 옵션

|상태|설명|
|:-------:|:------------------------------------------:|
|-l|프로세스 그룹 ID를 state 필드 앞에 출력|
|-n|프로세스 그룹 중에 대표 프로세스 ID를 출력|
|-p|각 프로세스 ID에 대해 한 행씩 출력|
|command|지정한 명령어를 실행|



---

### 4. kill 명령어

프로세스에 시그널을 보내는 명령어

* kill 리스트 확인

```vim
$ kill -l
```

* 주요 시그널

|시그널|영어|설명|
|:-----------:|:--------:|:------------------------------------------:|
|1) SIGHUP|Hang Up|세션이 종료될 때 시스템이 내리는 시그널|
|2) SIGINT|Interrupt|Ctrl + C, 종료 요청 시그널|
|9) SIGKILL|Kill|강제 종료 시그널|
|11) SIGSEGV|Segment Violation|메모리 침범이 일어날 때 시스템이 보내는 시그널|
|15) SIGTERM|Terminate|기본 값, 종료 요청 시그널|
|20) SIGTSTP|Temporary Stop|Ctrl + Z 일시 중지 요청 시그널|


---

---

## vim 에디터에서 매크로 사용방법에 대하여 조사하기 (q , @)

1) q[name]

2) ....(매크로 입력)

3) 매크로 종료 = q

4) 매크로 실행 = @[name]

5) 매크로 여러번 실행 = [number]@[name]
