# 알고리즘
## 디피
### 백준

1. 13302 리조트
- 풀이 : DP 를 이용한 최소값 구하기. 핵심은 함수 안에서 DP 를 사용할때, DP의 상태를 잘 파악해야한다.
- 근거 : 
1) idx > n 인 기저사례때는 0원 반환
2) dp 를 사용했는지 하지 않았는지에 따라 참조를 할지 새로 사용할지 확인
3) 사용할수 있는 날짜인지를 파악하는것이 필요
4) 함수의 상태에서 DP 를 저장을 어떻게 하느냐를 파악
5) 쿠폰이 3개가 모이면 하루 공짜
6) return 은 DP 를 반환함으로, 다음번의 상태가 현재의 상태와 영향을 주지 않음


핵심코드>
public static int payHotel(int idx,int cnt) {
		if(idx > n) return 0;
		if(dp[idx][cnt] != -1) return dp[idx][cnt];
		if(!check[idx]) return dp[idx][cnt] = payHotel(idx+1,cnt);
		
		dp[idx][cnt] = Math.min(10000+payHotel(idx+1,cnt),25000+payHotel(idx+3,cnt+1));
		dp[idx][cnt] = Math.min(dp[idx][cnt],37000+payHotel(idx+5,cnt+2));
		if(cnt>=3) dp[idx][cnt] = Math.min(dp[idx][cnt],payHotel(idx+1,cnt-3));
		return dp[idx][cnt];
	}

https://www.acmicpc.net/problem/13302
