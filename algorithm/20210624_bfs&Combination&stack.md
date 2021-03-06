# 알고리즘
## bfs & backtracking
### 백준

1. 14497 주난의 난(難)
- 풀이 : bfs 이지만, 추가적으로 depth 를 관리 해주면 됨.
0인 부분과 1인부분을 priorityqueue로 관리하며 가장 먼저 부딪힌 부분을 반환
- 근거 :
1) 레이어를 유지하며 최저 코스트일때의 값을 찾는것이 목적

https://www.acmicpc.net/problem/14497
2. 캠프 준비
- 풀이: 백트레킹, 재귀함수를 이용한 조합 문제
- 근거 :
1) n이 최대 15, 즉 2^n 을 해도 최대 2^15이상의 경우의 수는 나오지 않음

https://www.acmicpc.net/problem/16938

3. 괄호 제거
- 풀이 : 괄호의 index를 관리하는 배열을 선언함
- 애로사항 : 재귀함수 설계에 어려움이 있음. 또한, 괄호의 설계를 node 별로가 아닌 depth 별로 했기에 확실하게 되지 않음
- 근거 : 
1) 괄호 문제는 stack 을 사용하는것임. 즉, 재귀함수를 사용하여 풀수 있음.
2) 괄호를 분별할때 배열의 node 를 통해서 괄호를 점검

https://www.acmicpc.net/problem/2800
