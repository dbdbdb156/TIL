# 알고리즘
## 구현 & 디피 & 시뮬레이션 & 분할정복
### 백준

1. 1028 다이아몬드 광산
- 풀이 : dp 를 통해서 어떤부분을 저장할지를 나누는 것이 관건이였음.
좌측 대각선을 관리하는 배열과 우측 대각선을 관리하는 배열을 통해서 마름모를 점검
- 애로사항 : 시간복잡도 계산을 하지 못하여. 3중 O(n^3) 이 안될것이라고 생각함.
하지만, n = 750 이고, 최대길이의 n/2 길이만큼만 검색을 하기에 1억번 안의 연산에 끝남. 충분히 가능

https://www.acmicpc.net/problem/1028

2. 16236 아기 상어
- 풀이 : bfs와 우선순위 큐를 통한 다익스트라로 가장 빠른 물고기 찾기임
- 애로사항 :
1) 검색을 한 후에 배열의 값을 0 으로 초기화
2) 문제조건을 제대로 읽지 못함.(물고기를 상어의 크기만큼 먹어야 커짐)

https://www.acmicpc.net/problem/16236

3. 1992 쿼드트리
- 풀이 : 기본적인 분할정복 문제
- 애로사항 : row , col 을 관리하는 중간값을 따로 둬야 함. 두개의 값을 중복해서 사용하면 원치 않은곳을 참조하여 에러

https://www.acmicpc.net/problem/1992
