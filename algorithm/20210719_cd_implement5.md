# 알고리즘
## 구현
### 백준

1. 개구리 뛰기
- 풀이 : 전형적인 투포인터 문제
- 애로사항 : 처음에 이진탐색을 통해서 풀려고 했지만, 이진탐색은 안됨.
  1) 근거 : 이진탐색은 자료형이 연속적인경우에만 사용가능하다.
  2) 인덱스 관리의 어려움이 있었음

https://www.codeground.org/practice/practiceProblemViewNew

2. 방속의 거울
- 풀이 : 예외처리를 한 구현 문제

* 나눈 방법
// 왼오=0, 오왼 = 1, 위아 = 2, 아위 = 3;
// 왼오=0 + \ => 위아=2 , 왼오=0 + / = 아위=3;
// 오왼=1 + \ => 아위=3 , 오왼=1 + / = 위아=2;
// 위아=2 + \ => 왼오=0 , 위아=2 + / = 오왼=1;
// 아위=3 + \ => 오왼=1 , 아위=3 + / = 왼오=0;

https://www.codeground.org/practice/practiceProblemViewNew


-------------------
▲ 제대로 풀지 못한 문제
1. 균일 수
- 풀이 : 노가다로 품.

https://www.codeground.org/practice/practiceProblemViewNew
