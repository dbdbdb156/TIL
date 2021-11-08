# 가비지 컬렉션
- 정의 : JVM의 가비지 컬렉터(GC)가 불필요한 메모리를 알아서 정리.

##### ※ 참고
- 자바에서는 불필요한 데이터를 null 로 표현
- System.gc() 로 가비지 컬렉터를 호출할수 있지만 시스템 성능에 큰 영향을 줌으로 호출하면 안된다.

### * JVM heap 영역 설계 전제 2가지
- 객체는 대부분 일회성
- 메모리에 오랫동안 남아있는 경우 드물다
##### 1. 객체의 생존기간에 따라 물리적인 heap 영역을 나눔
1) young Generation
- 새롭게 생성된 객체가 할당되는 영역
- 대부분 객체가 금방 unreachable 되기에 많은 객체가 young 영역에 생성되었다가 사라짐
- young 영역에 대한 가비지 컬렉션을 Minor GC
2) old Generation
- young 영역에서 reachable 상태를 유지하여 살아남은 객체가 복사되는 영역
- 복사되는 과정에서 대부분 young 영역보다 크게 할당되며, 크기가 큰 만큼 가비지는 적게 발생한다.
- Old 영역에 대한 가비지 컬렉션을 Major GC 또는 Full GC

##### ※ Old 영역에 있는 객체가 Young 영역의 객체를 참조하는 것을 대비해, 512bytes의 카드 테이블 존재
; Old 영역에 있는 객체가 young영역의 객체를 참조할때마다 그에 대한 정보 표시
-> 카드 테이블만 조회하여 GC의 대상인지 식별

##### 2. Gabage Collecitons의 동작방식
young과 old 영역은 서로 다른 메모리 구조로 되어있어 작동은 다르지만 단계는 같음
1) stop the world : JVM이 애플리케이션의 실행을 멈추는 작업
; GC가 실행될때는 GC를 실행하는 쓰레드를 제외한 모든 쓰레드들의 작업이 중단 후, GC가 완료되면 작업이 재개
※ GC 성능 개선 : stop the world의 시간을 줄임.
2) mark and sweep
: stop the world 로 모든 작업이 중단되면 gc 는 모든 변수 or reachable 객체를 스캔하면서 각각 어떤 객체를 참고하고 있는지 탐색
- mark : 사용되는 메모리와 사용되지 않는 메모리를 식별하는 작업
- sweep ; mark 단계에서 사용되지 않음으로 식별된 메모리를 해제하는 작업



### * Minor GC 동작방식
 young 영역의 구조 : 1개의 eden , 2개의 survivor
- eden : 새로 생성된 객체가 할당되는 영역
- survivor 영역 : 최소 1번의 gc 이상 살아남은 객체가 존재하는 영역. 2개의 영역이지만 반드시 1개의 영역에만 데이터가 존재해야함.

i) eden 영역이 가득하면 Minor gc가 발생. 사용되지 않는 메모리는 해제, eden 영역에 존재하는 객체는 survivor 영역으로 이동.
ii) survivor 영역이 가득차게 되면, survivor 영역의 살아남은 객체를 다른 survivor 영역으로 이동시킨다( 즉, 1개의 영역은 반드시 빈 상태가 된다)
iii) 위 과정으로 살아남은 객체는 old 영역으로 이동
 Minor GC에서 객체가 살아남은 횟수를 의미하는 age를 object header에 기록하고 이를 보고 old 영역으로 이동을 결정한다

### * Major GC 동작방식
객체들이 계속 young에서 promotion 되어 old 영역 메모리가 부족해지면 발생
Young 영역은 old 영역보다 크기가 작음. 0.5~1초 사이에 끝남
but, olde 영역은 크기가 크고, young 영역을 참조할수도 있음. 10배이상의 시간을 사용함.

### * GC 최적화
 young 영역과 old 영역의 힙 크기를 알맞게 조정 : Trade-off
+ Minor GC가 지속되는 시간은 힙의 크기보다 GC에서 살아남는 객체들의 영향이 큼
; Eden -> survivor , survivor -> old 작업을 줄이는 것이 gc의 성능을 높임
(코딩의 영역이다)
1) Colleciton 의 크기를 예측설정해라 : collection 은 내부에 배열을 할당하고 크기가 바뀌면 가비지가 생긴다. 이걸 줄이자
2) Stream을 사용하라 : 파일, 네트워크로 데이터를 읽을 때.
- data 가 크면, OutOfMemoryErrors, 할당이 되도 이후 큰 규모의 가비지
=> InputStream을 직접 사용해라. InputStream 은 내부적으로 버퍼를 가지고 있다. 내부 버퍼 재사용으로 가비지 최소화하자
3) String 사용을 최적화 하라
i) 중복된 string 생성시, jvm 옵션을 사용 : UseStringDeduplication을 사용하며 String 인스턴스를 Global Single Char[] 로 관리하여 힙 메모리 사용 최적화
ii) StringBuilder를 사용하라. :
- Java9 부터는 invokedynamic으로 처리
4) 불변성(Immutablility)을 활용 : 가비지 컬렉터가 컨테이너 하위의 불변 객체들은 Skip할 수 있도록 도와준다. 왜냐하면 해당 컨테이너가 살아있다는 것은 하위의 불변 객체들 역시 처음에 할당된 그 상태로 참조되고 있다는 것을 의미
5) 불필요한 Collections 생성 피하기 : colleciton을 반환받을 때 메소드 내에서 컬렉션 객체를 생성해서 값을 채우고 변경이 불가능한 형태로 반환하는 것이 좋다.
but, colleciton addAll을 하면 불필요한 가비지를 생성한다.
-> 그러므로 파라미터로 colleciton을 넘겨줌으로 재사용하는 것이 메모리 낭비를 방지한다.
