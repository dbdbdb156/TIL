# 알고리즘
## 기타문제
### 백준

1. 1254 팰린드롬 만들기
- 풀이 : 문자열을 뒤집고 작은것부터 차근차근 문자열을 짤라서 확인하면 됨.
- 자바에서 문자열 바꾸는 방법 -> StringBuilder 에서 reverse 함수가 있음. or Char[] 선언해서 변환후 String 으로 변환

핵심코드>	
String rs = sb.reverse().toString();
		
		int i;
		for(i=0;i<s.length();++i) {
			if(s.substring(i).equals(rs.substring(0,s.length()-i))) {
				break;
			}
		}

https://www.acmicpc.net/problem/1254

2. 1092 배 ** 중요. ( 문자열 중에 어떤 것을 삭제하고 추가하는것은 LinkedList or ArrayList 를 사용해야함. 배열을 사용해서는 안됨)
- 풀이 : 정렬문제였음. 내림차순이든 오름차순이든 정리해서 list 안에 들어있는 값을 큰수 순서대로 제거하며 크레인의 크기만큼 찼으면 재 반복 

https://www.acmicpc.net/problem/1092

3. 1520 내리막 길
- 애로사항 : 풀었던 문제였음. 하지만 기억 나지 않음. 처음에는 bfs 로 풀려고 했음 하지만 문제가 있었음.
// bfs 를 사용할 경우 visited 를 사용하지 않는다면 여러 방향을 참조하는 bfs 특성상 중복 참조로 함수 스택이 터질수 있다.
// 위 문제 같은 경우는 역방향 dfs 를 이용해서 값을 참조하는것밖에 안된다. 즉, 역방향 dfs 를 dp 를 이용해서 할수 있는가를 물어보는 문제였다.
// 갔다가 도착을 했다면 dp 에 모두다 더해주는 형태로 내가 다녀왔다는것을 알려줄수 있다.
!! 가는 방향이 여러가지인 경우에 목적지의 수를 구할때 dp 를 이용한 dfs 가 유효하다.

https://www.acmicpc.net/problem/1520

4. 12764 싸지방에 간 준하
- 애로사항 : 우선순위큐를 어떻게 사용해야할지가 감이 안잡힘.
- 풀이 : 자리를 사용한 pq와 사용하지 않은 pq 를 관리해줌. 이를 통해서 자리를 다 사용하고 있다면, 새로운 자리를 추가해주고,
자리를 사용하고 사람들이 갔다면 간 자리를 추천해주면 됨.
핵심코드 >
PriorityQueue<use> use = new PriorityQueue();
		PriorityQueue<Integer> notuse = new PriorityQueue();
		int number =0;
		int front =0;
		for(int i=0;i<n;++i) {
			node nd = pq.poll();
			// front = 시작할 가장 앞 수
			while(!use.isEmpty() && nd.start > use.peek().end)
				notuse.add(use.poll().number);
			
			if(!notuse.isEmpty()) front = notuse.poll();
			else {
				front=number;
				number++;
			}
			if(usecheck.containsKey(front)) usecheck.put(front,(usecheck.get(front)+1));
			else usecheck.put(front,1);
			use.add(new use(nd.end,front));
			
		}

https://www.acmicpc.net/problem/12764
