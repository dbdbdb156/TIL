# 멀티 프로세스 대신 멀티 스레드를 사용하는 이유
- 프로그램 여러개를 키는 것 보다, 하나의 프로그램 안에서 여러작업을 해결하는 것이 편하기때문
### 1. 자원의 효율성 증대
- 멀티 쓰레드로 실행시 , 프로세스를 생성하여 자원을 할당하는 시스템 콜이 줄어들어 자원을 효율적으로 관리가 가능합니다.
 - 프로세스간의 Context Switching시 단순히 CPU 레지스터 교체뿐만 아니라 RAM과 CPU 사이의 캐시 메모리에 대한 데이터까지 초기화되므로 오버헤드가 크기 때문
### 2. 처리 비용 감소 및 응답 시간 단축
 - IPC(프로세스간 통신) 보다 스레드간의 통신 비용이 적으므로 작업간의 통신 부담 적음
 - 프로세스간의 전환속도보다 스레드간의 전환 속도가 빠름
  : Context Switching 시, stack 영역만 처리하면 됨.

### * Context Switching이란?
: 현재 실행되고 있는 Task(프로세스,쓰레드)의 상태를 저장하고 다음 진행할 Task의 상태값을 읽어 적용하는 과정
1) Task의 대부분 정보는 Register에 저장되고, PCB(process control block)로 관리
2) 현재 실행하는 Task의 PCB 정보를 저장하게 됨.(Process stack, Ready Queue)
3) 다음 실행할 Task의 PCB 정보를 읽어 Register에 적재하고 CPU 가 이전에 진행했던 과정을 연속적으로 수행할수 있음
* PCB 구조
- process state : 프로세스 상태(create,ready,running,waiting ,terminated)
- Process Counter : 다음 실행할 명령어의 주소값
- CPU Register : accumulator, stack pointers

### * Context Switching이 발생하게 되면 많은 Cost가 소요됩니다.
 - Cache 초기화
 - Memory Mapping 초기화
 - Kernel은 항상 실행되어야 합니다.(메모리 접근을 위해서)

=> 쓰레드보다 프로세스 Context Switching coas 가 많이 듭니다.
근거
- thread 는 stack 영역을 제외한 모든 메모리를 공유하기 때문
- Context Switching 발생시 stack 영역만 변경을 진행하면 됨.

But, 멀티 쓰레드 환경에서는 자원을 공유하기 때문에, 동기화 문제
