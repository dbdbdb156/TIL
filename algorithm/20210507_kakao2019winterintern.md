# 알고리즘
## 구현
### 카카오

1. 크레인 인형뽑기 
- 간단한 구현 : row 의 마지막부터 값이 쌓이기에, length[] 배열은 임의로 둬 인덱트 참조에 이용

https://programmers.co.kr/learn/courses/30/lessons/64061

2. 튜플
- 값을 순서대로 참조하기 위해서 check 배열을 선언. 값이 있으면 다른값 참조
- 순서는 작은값부터 순서대로
- ArrayList 로 배열의 순서를 담고있는 배열 사용
- 람다식을 이용해서 풀수도 있었음
-> Arrays.sort(list,(a,b)-> return a.length()-b.length());

https://programmers.co.kr/learn/courses/30/lessons/64065

3. 불량 사용자
- 백트레킹을 사용했을때 중복을 포함하여 값이 제대로 나오지 않음.
- Set을 이용해서 비트마스크 형식으로 유니크한 값을 저장하여 중복을 체크함.

https://programmers.co.kr/learn/courses/30/lessons/64064

-> 카카오는 문자열 구현문제가 많음.
