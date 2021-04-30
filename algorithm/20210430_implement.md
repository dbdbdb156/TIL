# 알고리즘
## 구현 & BFSd
### 백준

### 1. 1261 : 알고스팟
- 풀이 : bfs로 4방향 탐색 및 Queue 는 PriorityQueue 로 구현.
- 원래의 목적은 Deque 로 구현이지만, 벽의 특성상 weight 를 search 기준으로 두고 우선순위 큐를 구현이 더 효율적이라 생각함.
- 애로사항 : 그냥 bfs 실행시 벽을 부딪히는 것도 염두에 두고 실행해버림.
즉, visited 를 벽이 있는 곳에서 bfs 를 실행함으로 원래 원했던 값이 나오지 않음.

https://www.acmicpc.net/problem/1261


-------------------
### 풀지못한 문제

##### 2. 14719 빗물
생각해본 풀이
1) row를 기준으로 올라가면서 구현
2) col을 기준으로 밀어가면서 높은 값을 찾으면 구현
3) 높아질때마다 index 를 기준으로 sum을 더하며 구하기

https://www.acmicpc.net/problem/14719

#### 3. 1717 : 집합의 표현
- Union find 로 푸는건 알겠지만, 왜 집합으로 풀었을때는 에러가 뜨는지에 대해서 파악중이다.
-> Union find 로 먼저 구현하고 집합으로 풀었을때 합집합이 왜 안되는지에 대해서 파악해보기

https://www.acmicpc.net/problem/1717
