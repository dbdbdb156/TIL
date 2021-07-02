# Spring 기본 상식

* gradle, maven 의존관계 다 당겨준다
* 참고)
- Log 가 궁금하다면 두가지를 검색해라
1)junit
2)springtest 

### 정리
* spring-boot-starter-web 라이브러리
1) tomcat(웹서버)
2) 스프링 웹 MVC 가 들어가있다.
* spring-boot-starter : 스프링 부트 + 스프링 코어 + 로깅
* 
* 로깅:
1) slf4j : 인터페이스
2) logback

* 테스트 라이브러리 : Spring boot starter-test
1) junit
2) mockito 라이브러리
3) assertj : 테스트 코드를 좀 더 편하게 작성하게 도와주는 라이브러리
4) spring-test : t스피링 통합 테스트 지원


---------------------
#  컨트롤러 설정
@Controller
@ GetMapping("hello")

- Controller 단의 Model 변수가, templates 파일의 html 파일의 ${data} 에 연결됨. 변수이름
- Controller의 @GetMapping 된 함수의 return 값은 templates 파일의 hello.html 파일의 이름과 같다
=> Controller 에서 리턴값으로 문자를 반환하면 뷰 리졸버(viewResolver)가 html 파일을 찾아서 화면에 출력

## 검색해보기 : Srping-boot-devtools 
** 서버 배포할때는 이 파일만, 파일만 복사해서 붙여넣으시고, java -jar 실행시키면 서버가 실행되는거다.
: 그러면 서버에서도 스프링이 실행되게 된다.
* builde 방법
cmd : gradlew build -> cd build, cd libs -> java -jar fildname.jar 순서이다.

## 출력 종류
1. 정적 컨텐츠 : 파일을 그대로 파일에 내려주는것
2. MVC 와 템플릿 엔진 : jsp, php
서버에서 프로그래밍해서 동적으로 내리는것
: 그것 떄문에 MVC 모델 뷰 컨트롤러로 개발하는것
3. API : 안드로이드, 아이폰 개발하면
요즘은 json 으로 데이터 구조 포맷으로 클라이언트에게 보낸다. 그게 요즘 방법이다.
vue, react 사용하는것, 서버끼리 통실할떄, html 내릴 필요가 없기에, 서버끼리 그리 통신한다

## 1. 정적 컨텐츠 : 자동지원
-> 스프링에 넘기면, 스프링은 controller 에서 먼저 찾아본다. 그런 컨트롤러 없으니까, 
2. 내부의 resource 의 파일을 찾는거다.

---------------------------
## 2. MVC 템플릿 엔진
* VIEW 는 관심사를 분리해야한다.
- VIEW 는 화면을 그리는데 온 집중을 다해야한다.
<->
- Controller,Model은 비즈니스 로직 or 내부적인것을 처리하는데 집중해야한다.

* viewResolver : 화면과 관련된 해결자
: view 를 찾아주고 ,templeate 엔진 연결 해주는거다.

------------------
## 3. API 
@ResponseBody 의미 :  http 에서 헤더, 바디 부에, 직접 바디부에 넣겠다는 의미다.
String 이라면 , hello spring 으로 갈것이다.

Q 만약 @ GetMapping에 객체를 넘기면 어떻게 되나요?
-> JSON 방식으로 나옵니다.

**
@ResponseBody 가 없으면
1) ViewResolver 에 던진다. 즉 템플릿의 html 파일을 확인한다.

@ResponseBody 가 있으면 HTTP BODY에 문자 내용을 직접 반환
1) 문자열 = 그냥 바디에 담아서 반환
StringConverter
2) 객체 : JSON 으로 만들어서 반환
JSONConverter
-> HttpMessageConverter 가 동작한다.
