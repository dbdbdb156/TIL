# 1. JVM
 ## 자바 컴파일 순서
  1) 개발자가 자바 소스코드(.java)를 작성
  2) 자바 컴파일러가(java complier)가 자바 소스파일 컴파일.
    java -> .class 파일 생성(자바 가상 머신이 읽을수 있는 바이트 코드)
    바이크 코드의 명령어 = Opcode(1Byte) + 추가 피연산자
  3) 컴파일된 바이트코드(java byte code)-> 클래스로더(class loader)
  4) 클래스 로더 : 동적로딩(Dynamic loading)을 통해 필요한 클래스 로딩 및 링크
	=> 런타임 데이터 영역(Runtime data area)에 적재‘ = JVM 메모리에 올림
	즉, 자바는 컴파일 시점이 아닌 런타임 시점에 클래스를 처음으로 참조하며 해당클래스를 로드하고 링크하는 동적로드의 특성을 가짐. 동적로드를 담당하는 것이 JVM의 클래스 로더
   * 클래스 로더가 로드하지 않은 클래스 찾으면 세부 동작
	a. 로드 : 클래스 파일을 JVM 메모리에 로드
	b. 검증 : 자바 언어 명세(java language specification) 및 JVM 명세에 명시된 대	로 구성되어 있는지 검사
	c. 준비 : 클래스가 필요로 하는 메모리를 할당( 필드,메서드, 인터페이스 등등)
	d. 분석 : 클래스의 상수 풀 내 모든 심볼릭 레퍼런스를 다이렉트 레퍼런스로 변경
	e. 초기화 : 클래스 변수들을 적절한 값으로 초기화합니다(static 필드)

   - 컴파일된 java byte code가 클래스 로더에 의해 Runtime data area에 적재되고, execution engine(실행 엔진)을 통해서 자바 바이트 코드를 실행한다.
	-> 자바 바이트 코드는 Excution Engine을 통해 런타임 시점에 실행 된다

## 특징
  1) 스택 기반의 가상 머신
    : 레지스터 기반이 아닌 스택기반으로 동작
  2) 심볼릭 레퍼런스
   - 기본 자료형을 제외한 모든 타입(클래스와 인터페이스)을 명시적인 메모리 주소 기반의 	레퍼런스가 아닌 심볼릭 레퍼런스를 통해 참조한다
  3) 가비지 컬렉션
   - 클래스 인스턴스는 사용자 코드에 의해 명시적으로 생성되고 가비지 컬렉션에 의해	자동으로 파괴된다.
  4) 기본 자료형을 명확하게 정의하여 플랫폼 독립성 보장
   - c/c++ 과 다르게 기본 자료형을 명확히 정의하여 호환성 유지와 플랫폼 독립성 보장
  5) 네트워크 바이트 오더(network byte order)
   - 자바 클래스 파일은 네트워크 바이트 오더를 사용. 인텔 x86 아키텍처가 사용하는 리틀 엔디안, RISC 계열 아키텍처가 사용하는 빅 엔디안 사이에서 플랫폼 독립성을 위해 고정된 바이트 오더를 유지하기 위해 네트워크 전송시에 사용하는 바이트 오더인 네트워크 바이트 오더를 사용한다. = 네트워크 바이트 오더는 빅 엔디안

### Runtime data Area 
: JVM이 운영체제 위에서 실행되면서 할당받은 메모리 영역. 즉, 자바 메모리 영역
- 런타임 데이터 영역 6개
#### 쓰레드마다 차지하는 영역
1) PC Register : 현재 실행중이 JVM명령의 주소를 가짐
2) JVM stack : 각 쓰레드마다 하나씩 존재, 스택 프레임이라는 구조체를 저장하는 스택.
JVM은 오직 JVM stack 프레임을 추가하고 제거하는 동작만 수행한다.
3) Native Method stack : 자바 외의 언어로 작성된 native d코드를 위한 스택, JNI(java native interface)를 통해 호출하는 C/C++ 등의 코드를 수행하기 위한 스택으로, 언어에 맞게 C 스택이나 c++ 스택이 생성된다.

#### 모든 쓰레드가 공유하는 영역
4) heap : 인스턴스 또는 객체를 저장하는 공간, 가비지 컬렉션의 대상. JVM 성능 등의 이슈에서 가장 많이 언급되는 공간.
5) method area : class area,static area
- JVM이 시작될 때 생성. JVM이 읽은 클래스,인터페이스에 대한 런타임 상수 풀, 필드, 메서드 정보, static변수, 메서드의 바이트코드 등을 보관
6) runtime constant pool : 클래스 파일 포맷에서 constant_pool 테이블에 해당하는 영역
메서드 영역이 포함되는 영역. JVM명세에서도 따로 기술할 정도로 중요
=> 각 클래스와 인터페이스의 상수뿐 아니라, 메서드와 필드에 대한 모든 레퍼런스 담고있는 테이블

##### ※ 리틀 엔디안 vs 빅 엔디안
- 엔디안 : 컴퓨터 메모리 같은 1차원 공간에 여러개의 연속된 대상을 배열하는 방법
- 빅 엔디안 : 큰 단위가 앞에 나옴. 즉, 최상위 바이트부터 차례로 저장
; 디버그가 편함. 사람이 사용하는 방식과 같음. 비교연산에서 빠름
- 리틀 엔디언 : 작은 단위가 앞에 나옴. 즉, 최하위 바이트부터 차례로 저장하는 방식
; 메모리에 저장된 값의 하위 바이트들만 사용할 때 별도의 계산이 필요없음. 계산빠름
- 미들 엔디언 : 둘다 지원

### Class loader(클래스로더)
* 클래스로더 우선순위 : Bootstrap > Extention > System
1) 계층 구조 : 클래스 로더끼리 부모-자식 관계를 이루어 계층 구조로 생성
최상위 클래스 로더는 부트스트랩 클래스 로더(Bootstrap class loader)
2) 위임 모델 : 계층 구조를 바탕으로 클래스 로더끼리 로드를 위임하는 구조로 동작.
클래스 로드시 먼저 상위 클래스 로더를 확인하여 있으면 사용, 없다면 로드를 요청 받은 클래스로더가 클래스를 로드한다.
3) 가시성 제한 : 상위 클래스 로더는 하위 클래스로더의 클래스를 받을수 없음
4) 언로드 불가 : 클래스 로더는 클래스를 로드할수 있지만 언로드할수 없다.
언로드 대신 현재 클래스 로더를 삭제하고 아예 새로운 클래스 로더를 생성 가능
