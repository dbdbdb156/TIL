# 알고리즘
## 구현
### 백준
1. 17413	단어 뒤집기 2
https://www.acmicpc.net/problem/17413

2. 16926	배열 돌리기 1
https://www.acmicpc.net/problem/16926

3. 20207	달력
https://www.acmicpc.net/problem/20207

4. 16395 파스칼의 삼각형
- 풀이 : 배열을 통한 dp 사용
핵심코드>
Arrays.fill(map,1);
		for(int i=1;i<n;++i) {
			for(int j=i;j>1;--j) {
				map[j]=map[j]+map[j-1];
			}
		}

https://www.acmicpc.net/problem/16395

5. 1068 트리
- dfs 를 이용, flag 를 이용해 노드를 한번도 방문하지 않았다면 리프
핵심코드>
public static void dfs(int index) {
		visited[index] = true;
		boolean flag = false;
		ArrayList<Integer> v = list.get(index);
		for(int i=0;i<v.size();++i) {
			if(!visited[v.get(i)]) {
				visited[v.get(i)] = true;
				dfs(v.get(i));
				flag =true;
			}
			
		}
		if(!flag) sum++;
		
		
	}

https://www.acmicpc.net/problem/1068


--------------------------------
### 백준
- 풀지못한 문제
1. 2293 https://www.acmicpc.net/problem/2293
2. 1261 https://www.acmicpc.net/problem/1261













