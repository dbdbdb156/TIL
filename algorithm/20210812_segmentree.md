# 알고리즘
## 세그먼트 트리 & 다익스트라
## 프로그래머스 & 백준

1. 경주로 건설
- 풀이 : 다익스트라를 사용하되, 방향에 따른 dp 를 더 설정해야함.
- 근거 : 한 정점에 관해서 들어오는 화살표와 나가는 화살표를 검증하기 위해서는 각자 다른 화살표에 따른 메모라이제이션이 필요하다.

https://programmers.co.kr/learn/courses/30/lessons/67259


2. 11505 구간 곱 구하기
- 풀이 : 세크먼트 트리
- 애로사항 : 세크먼트 update 를 구현할때, 0인 가중치인 경우 다른수로 변동하기 어렵다.
즉, 모든 값을 재귀 형태로 최신화 해주면 된다.

https://www.acmicpc.net/problem/11505


























