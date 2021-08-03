# 알고리즘
## 구현
### 백준

1. 1013 Contact
- 풀이 : 정규식 사용.
* 참고 : 정규식
+ : 1개이상
? : 0~1개
* : 0개이상
| : 또는

핵심코드>
String s = br.readLine();
String pattern = "(100+1+|01)+";
if(s.matches(pattern)) sb.append("YES").append("\n");

https://www.acmicpc.net/problem/1013

2. 20055 컨베이어 벨트 위의 로봇
- 풀이 : 구현, 구현에서 원하는 바를 차근차근 실행.

https://www.acmicpc.net/problem/20055

3. 2140 지뢰찾기
- 풀이 : # 을 기준으로 8방향 검색, 주변이 0이면, 지뢰가 없음.
모든방향에 지뢰가 있다면, 즉 지뢰가 없는 부분이 없다면, 무조건 지뢰가 있는것이기에,
모든 방면의 값을 낮춰주면 된다.

https://www.acmicpc.net/problem/2140
