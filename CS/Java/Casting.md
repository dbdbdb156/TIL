# Casting(업캐스팅 & 다운캐스팅)
### * 캐스팅 필요한 이유 :
1) 다형성 : 오버라이딩된 함수를 분리해서 활용할수 있다.
2) 상속 : 캐스팅을 통해 범용적인 프로그래밍이 가능하다.

### * 형변환의 종류 :
1) 묵시적 형변환 : 캐스팅이 자동으로 발생(업캐스팅)
ex) Parent p = new Child();
-> 부모를 상속받은 child 는 Parent를 포함하고 있음
2) 명시적 형변환 : 캐스팅할 내용을 적어줘야 하는 경우(다운캐스팅)
ex) Parent p = new child();
Child c = (Child) p
: 다운캐스팅은 업 캐스팅이 발생한 이후에 작용한다.

- 자바에서는 오버라이딩된 함수를 동적 바인딩 하기 때문에, child를 참조한다.
- 자식에 부모를 할당할수 없다.
ex) Child c = (child) new Parent();