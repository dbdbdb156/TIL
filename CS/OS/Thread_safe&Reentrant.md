# Thread-safe : 쓰레드 안전, 쓰레드 세이프
- 멀티 쓰레드 환경 : 여러 쓰레드가 동시에 하나의 공유자원에 접근할 때 의도한대로 동작하게 하는 것
* 공유 자원에 접근하는 임계영역(Critical section)을 동기화 기법으로 제어해줘야한다.
= 상호배제
=> 방법 : 뮤텍스, 세마포어

### * Reentrant : 리엔트런트
 - 재진입성 : Reentrant 하다 = 여러 스레드가 동시에 접근해도 언제나 같은 실행 결과는 보장한다.
; 서브루틴에서는 공유자원을 사용하지 않으면 된다.
 - 호출시 : 제공된 매개변수로만으로 동작해야 한다.
 - 재진입이 가능하면 쓰레드 세이프하지만 그 역을 성립하지 않는다.