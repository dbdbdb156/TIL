# 알고리즘
## 세그먼트 트리
### 백준

1. 2042 구간 합 구하기
- 풀이 : 전형적인 세그먼트 트리 사용
- 근거 : 
1) n = 100만, O(n^2) 의 시간 복잡도로는 시간초과이다.
2) 만약 prefixSum 을 사용했다면, index 가 n의 마지막 인덱스라면, update 를 할때마다 n 만큼의 부분합의 변동이 있어야 한다.
-> 즉, 100만 * 1만 = 100억번 즉, 시간초과
3) 그러므로 log 의 시간복잡도인 자료구조가 필요함

https://www.acmicpc.net/problem/2042

-------------------------------
### 참고
* 세그먼트 트리
- 여러개의 데이터가 연속적으로 존재할때 부분합을 빨리 구할수 있는 방법
- 메모리에는 n*4 의 메모리가 필요.
- 펜윅 트리 <-> 세그먼트 : 팬윅트리가 메모리 관리 차원에서 더 좋음. 펜윅트리는 n 의 메모리만 있으면 됨.

- 3가지의 구현부 :
1) 트리구성
2) update
3) 부분합

<핵심코드>
public static long makeSegmentTree(int start,int end,int node) {
		if(start==end) return seg[node] = num[start];
		int mid = (start+end)/2;
		return seg[node] = makeSegmentTree(start,mid,node*2)+makeSegmentTree(mid+1,end,node*2+1);
	}
	public static long sum(int start,int end,int node,int left,int right) {
		if(left > end || right < start) return 0;
		if(left <= start && end <= right) return seg[node];
		int mid = (start+end)/2;
		return sum(start,mid,node*2,left,right) + sum(mid+1,end,node*2+1,left,right);
	}
	public static void update(int start,int end,int node,int idx,long diff) {
		if(idx < start || idx > end) return ;
		seg[node] += diff;
		if(start==end) return ;
		int mid = (start+end)/2;
		update(start,mid,node*2,idx,diff);
		update(mid+1,end,node*2+1,idx,diff);
	}
