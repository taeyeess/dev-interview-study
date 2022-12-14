Interrupt

장치에 예외상황이 발생하여 급하게 처리가 필요할 경우에 CPU가 실행하고 있던 프로그램을 가로막고 예외상황을 처리할 수 있도록 하는 것

​

인터럽트의 종류

내부 인터럽트

수식을 0으로 나누거나, 비정상적인 메모리에 접근하는 등 SW적 예외 상황이 발생하는 경우

외부 인터럽트

CPU 코어 외부에서 어떤 일이 발생한 것을 전기적인 신호로 CPU에게 통지하는 경우 

​

하드웨어 인터럽트

하드웨어가 발생시키는 인터럽트로, CPU 외부의 하드웨어 장치에서 cpu에 오는 인터럽트 요구 신호에 의해 발생

Maskable interrupt

Non-maskable interrupt

Interrupt Mask(인터럽트가 발생하였을 때 요구를 받아들일지 말지 지정하는 것)

-가능

-불가능

인텔 CPU에서 INTR pin으로 신호가 들어옴

인텔 CPU에서 NMI pin으로 신호가 들어옴

정전, 하드웨어 고장 등 어쩔 수 없는 오류

하드웨어 인터럽트 종류

입출력 인터럽트 (I/O interrupt)

정전,전원 이상 인터럽트(Power fail interrupt)

기계 착오 인터럽트(Machine check interrupt)

외부 신호 인터럽트(External interrupt)

​

소프트웨어 인터럽트

사용자가 프로그램을 실행시키거나 Supervisor(=OS) 를 호출(SVC=SuperVisor Call)하는 동작을 수행하는 경우

소프트웨어(사용자 프로그램)가 스스로 인터럽트 라인을 세팅하여 발생시키는 인터럽트

CPU 내부에서 자신이 실행한 명령이나 CPU의 명령 실행에 관련된 모듈이 변화하는 경우 발생

trap 또는 exception 이라고도 함

프로그램의 오류에 의해 생기는 인터럽트

​

소프트웨어 인터럽트 종류

프로그램 검사 인터럽트 (Program check interrupt) 

0으로 나누는 경우

OverFlow/UnderFlow

페이지 부재

부당한 기억장소의 참조

SVC(Supervisor Call: 감시프로그램 호출)인터럽트

인터럽트 우선순위 판별 방법

폴링 (Polling)

요청을 주기적으로 검사하여 상태가 변화했을 때 ISR 을 수행하는 소프트웨어적인 방법

인터럽트를 조사하는 비용이 들어 반응시간이 느리지만, 하드웨어를 추가할 필요가 없어 회로가 간단함

데이지 체인 (Daisy Chain)

 어디에 인터럽트가 발생하는지 확인하는 회로를 직렬로 연결하는 하드웨어적인 방법 


관련 용어

인터럽트 서비스 루틴   Interrupt Service Routine(ISR)

인터럽트 핸들러 Interrupt handler라고도 함

운영체제의 코드 영역에는 각각의 인터럽트에 대응하여 처리해야 할 기계어 코드 루틴(커널이 실행)이 프로그램되어 있음

CPU에서 인터럽트가 접수되면, 해당 인터럽트 핸들러 코드의 위치를 찾고 기계어  코드 루틴을 실행에 옮김. 실행 중이던 레지스터와 PC를 보관함으로써 CPU의 상태 보존, 인터럽트가 핸들링이 완료되면 이전의 상태로 복귀

인터럽트 벡터   Interrupt Vector

인터럽드 발생 시 처리해야 할 루틴(ISR)의 주소를 인터럽트 별로 보관하고 있는 테이블

PCB(Process Control Block)

커널의 데이터 영역에 존재하며 각각의 프로세스마다 고유의 PCB가 있음

인터럽트 발생 시 프로세스의 어느 부분이 수행중이었는지 저장

PC (Program Counter)

CPU 내부에 있는 레지스터 중의 하나로서, 다음에 실행될 명령어의 주소를 가지고 있어 실행할 기계어 코드의 위치를 지정하며 명령어 포인터라고도 함

시스템 콜 System Call

주소 공간 자체가 다른 곳(커널의 code영역)으로 이동해야 하므로 프로그램이 인터럽트 라인에 인터럽트를 세팅하는 명령을 통해 이루어진다. 즉, 하드웨어적으로 모드 비트가 1에서 0으로 자동으로 세팅되어 특권 명령을 수행할 수 있게 된다.

 

명령어의 종류

CPU가 수행하는 명령에는 일반 명령과 특권 명령이 있다.

일반 명령은 메모리에서 자료를 읽어오고, CPU에서 계산을 하는 등의 명령이고 모든 프로그램이 수행할 수 있는 명령이다.

특권 명령은 보안이 필요한 명령으로 입출력 장치, 타이머 등의 장치를 접근하는 명령이다. 특권 명령은 항상 운영체제만이 수행할 수 있다.

​

kernel mode vs user mode

운영체제는 하드웨어적인 보안을 유지하기 위해 기본적으로 두가지 operation을 지원한다. kernel mode는 운영체제가 CPU의 제어권을 가지고 명령을 수행하는 모드로 일반 명령과 특권 명령 모두 수행할 수 있다.

user mode는 일반 사용자 프로그램이 CPU제어권을 가지고 명령을 수행하는 모드이기 때문에 일반 명령만을 수행할 수 있다.

user mode가 디스크 입출력 명령을 읽었지만 특권 명령을 수행할 수 없으므로 현재 수행중인 사용자 프로그램을 잠시 멈추고 운영체제에게 시스템 콜을 통해 특권명령을 대신 수행해달라고 요청하여 CPU의 제어권을 양도한다(kernel mode).

​

 인터럽트 과정

process A 실행 중 디스크에서 어떤 데이터를 읽어오라는 명령을 받았을 때

process A는 system call을 통해 인터럽트를 발생시킨다.

CPU는 현재 진행 중인 기계어 코드를 완료한다.

현재까지 수행중이었던 상태를 해당 process의 PCB(Process Control Block)에 저장한다. 

PC(Program Counter, IP)에 다음에 실행할 명령의 주소를 저장한다.

인터럽트 벡터를 읽고 ISR 주소값을 얻어 ISR(Interrupt Service Routine)로 점프하여 루틴을 실행한다.

해당 코드를 실행한다.

해당 일을 다 처리하면, 저장했던 프로세스 상태 복원한다.​

ISR의 끝에 IRET 명령어(이전 task(작업단위의 실행단위)로 다시 돌아가는 어셈블리 명령어. ISR의 마지막 명령어.)에 의해 인터럽트가 해제 된다.

IRET 명령어가 실행되면, 대피시킨 PC 값을 복원하여 이전 실행 위치로 복원한다.

 


 

 

참고

https://huistorage.tistory.com/111

https://medium.com/@lazypanda43/%EC%9D%B8%ED%84%B0%EB%9F%BD%ED%8A%B8-%EC%A2%85%EB%A5%98%EC%99%80-%EC%B2%98%EB%A6%AC%EA%B3%BC%EC%A0%95%EA%B3%BC-%EC%9A%B0%EC%84%A0%EC%88%9C%EC%9C%84-c95c26909472

https://velog.io/@adam2/%EC%9D%B8%ED%84%B0%EB%9F%BD%ED%8A%B8

https://otakuking.tistory.com/70

https://docs.oracle.com/cd/E19455-01/806-3773/instructionset-75/index.html

https://wiki.kldp.org/Translations/html/The_Linux_Kernel-KLDP/tlk7.html

https://docs.aws.amazon.com/ko_kr/freertos-kernel/latest/dg/interrupt-management.html

http://openclass.pe.kr/read.cgi?board=databank&y_number=25