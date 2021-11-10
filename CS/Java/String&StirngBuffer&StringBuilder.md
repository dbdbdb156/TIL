# String, StringBuffer, StringBuilder 차이


|---|String|StringBuffer|StringBuilder|
|---|---|---|---|
|변경|Immutable|mutable|mutable|
|동기화||Synchronized 가능(Thread-safe)|Sychronized 불가능|

## 1. String
- new 연산으로 생성된 인스턴스 메모리 공간 변동 없음
- Garbage Collector로 제거 되야함
- 문자열 연산시 새로 객체를 만드는 Overhead 발생
- 객체가 불변하기에, 멀티쓰레드에서 동기화 신경 쓸 필요 없음(조회 연산에 장점)

## 2. StringBuffer, StringBuilder 특징
#### * 공통점
 - new 연산으로 클래스를 한번만 만듬
 - 문자열 연산시 새로 객체를 만들지 않고 크기를 변경시킴
 - StringBuilder 와 StringBuffer 메서드 동일
#### * 차이점
 - StringBuffer : Thread_safe (문자열 연산이 많은 멀티쓰레드 환경) 
 - StringBuilder : Thread-safe 하지 않음 (문자열 연산이 많은 Single-Thread or Thread에 연관되지 않은 환경)
