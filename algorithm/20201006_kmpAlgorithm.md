# KMP(Knuth–Morris–Pratt) Algorith
## 목적: 검색 문자열과 타켓 문자열간 검색 시간 최소화
; 같은 문자열, 리버스 된 문자열 등
### 과정
: pi[] 배열을 먼저 계산후, 각자 자리별 얼마나 맞는지 확인,
전체 문자열을 보며 검사 문자열이 포함되는지를 확인
(pi 배열은 접두 문자열과의 중복수준을 길이로 표현,
추후 같지 않을때, 안되는 문자열을 뛰어넘고 되는 문자열 검색시 사용)

#### 핵심로직
begin, match 변수
while(begin + match < 타켓 문자열의 길이)
  if( 검색 문자열 = 타켓 문자열 간 동일 확인)
  {
    ++match;
    // 필요한 업무 처리
  }
  else{
     // 같은 문자열이 없는경우 다음 위치로 넘어감
    if(match == 0 ) begin ++;
    // 같은 문자열은 없지만, match 되는 부분이 몇개 있을때
    else{
      // 다음 동일한 부분(접미 인덱스 저장)
      begin += mathch -pi[match-1] ; 
      // match 를 통해 이미 계산된 거리만큼은 건너뜀.
      match = pi[match -1];
    }
  
  }
  
  ### 의의 :
  장점 : 
  - 문자열 검색에 시간 단축이 됨.
  - 배열간 검색에서는 언제든 사용하다는 점
  단점 :
  - 코드는 직관적이지 않은편
  
  ** 코드 문제도 풀어봐야 함.
 --------------------------------------------------------------------
 
 ## 별개
 - 공부를 하였지만, 문제를 풀지 못한 경우에는 TIL 를 올리지 않음
 문제점) 내가 공부를 했다는 것이 체감이 안됨.
 해결방안) 공부를 조금하고, 풀리지 않은 문제도 다음날 풀수 있도록 기록하는방향
 
 
 
 
 
 
  
