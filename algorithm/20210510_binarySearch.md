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


3. 2110 공유기 설치
- 풀이 : 이분탐색, 위의 두문제와 다르게, 이분탐색의 탐색 값을 집간의 거리 house[i] - start = d 로 두어
- mid 값인 최소거리값을 유지하는지 확인한다.
* 애로사항:
1) 데이터의 크기를 볼떄 항상 21억이 넘는지 봐야한다. long 과 int 값 범위 확인
2) mid 값을 어떤것을 binary search 할지를 확실히 정하지 않으면 힘들다.
3) 최대 길이를 구할떄 house[n] - house[0] = 제일 긴길이이다. index를 1부터 시작했기에 n-1 이 최대값이 아닌, n 배열인덱스가 최고이다. (sorting 했을때)

https://www.acmicpc.net/problem/2110


------
