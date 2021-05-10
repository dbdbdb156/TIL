# 알고리즘
## Binary Search
### 백준

1. 2085 나무 자르기
- 풀이 : 파라메트릭 서치를 통한 이분탐색
배열들은 sorting이 되어있어야함. 즉 연속적이여야함.
https://www.acmicpc.net/problem/2805

핵심코드>
public void searchtree(long left,long right) {
		
		if(left > right) return ;
		long mid = (left+right)/2;
		
		long cnt =0;
		for(int i=1;i<=n;++i) {
			if(tree[i]>mid) {
				cnt+= tree[i]-mid;
			}
			if(cnt >= m) {
				break;
			}
		}
		// 통과됬다
		if(cnt >= m) {
			max = Math.max(max,mid);
			searchtree(mid+1,right);
		}
		else {
			searchtree(left,mid-1);
		}
		
	}

2. 1654 랜선 자르기
- 위 풀이와 동일
https://www.acmicpc.net/problem/1654

------
