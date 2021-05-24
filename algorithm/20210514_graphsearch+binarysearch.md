# 알고리즘
## dfs + binarysearch
### 백준

1. 1939 중량제한
- 풀이 : 이분탐색을 이용해서 지나갈수 있는 값 mid를 정한다음 dfs or bfs 로 할수 있는지 확인한다
- 근거
1) 데이터의 중량이 10억이였음 + 다익스트라는 메모라이제이션을 통해서 가는 가중치의 합을 저장하는데, 그렇지 않음.
- 애로사항
1) bfs 에서 오류가 뜸 : 문제 자체를 제대로 이야하지 못함. 조건이 들리지 않았고(check) + mid 값 보다 간선이 크거나 같아야함. 두가지 조건을 다 만족해야 이동을 할수 있음
-> 
3) bfs 보다 dfs 가 더 빠른 이유. 있는 결과값을 찾아가는 것이기에 bfs 는 모든 노드를 훑고 지나가고 dfs 는 같은 노드를 지나지만 답만 찾으면 함수를 끝내버림

dfs 핵심코드>
public static boolean dfs(int index, int mid) {
		
		if(index == end) {
			return true;
		}
		check[index] =true;
		for(int i=0;i<list.get(index).size();++i) {
			if(list.get(index).get(i).w>=mid) {
				if(!check[list.get(index).get(i).v]) {       <- 원래는 여기위에 check 배열을 선언 해두었음. 그러니 체크가 되지 않는데도 그냥 dfs 를 실행시켜 의도치 
					if(dfs(list.get(index).get(i).v,mid)) {
						return true;
					}
				}
				
			}
		}
		return false;
	}


https://www.acmicpc.net/problem/1939

* 재귀 함수를 쓸때 유의사항
1) return 값이 꼭 함수이지 않아도 된다.
2) 함수 자체의 상태를 기억해야한다.
3) 함수 자체가 조건으로 들어갈수도 있다. 그럴경우에는 조건을 다르게 줘도 된다.

