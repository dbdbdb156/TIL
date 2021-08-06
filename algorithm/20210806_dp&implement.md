# 알고리즘
## 구현 및 디피
### 백준

1. 18222 투에-모스 문자열 
- 풀이 : dp를 이용하여 2의 배수의 자리가 되는 수들의 자리값을 저장하여 사용하는 형태로 사용함.
즉, 시간은 O(logN) 임. 구현에서 어려움이 있었지만, Map을 이용해서 값을 처리.

https://www.acmicpc.net/problem/18222

2. 21737 SMUPC 계산기
- 풀이 : 구현문제, 값을 저장하는 q 와 연산자를 저장하는 q를 이용해서 연산
- 애로사항 : 처음에 시간초고과 남. 이유는 ArrayList<> 의 remove 함수를 사용했었는데, 배열을 지우는 것이기에 O(n) 의 시간을 사용해서
풀이의 시간복잡도가 O(n^2) 이 되어버렸음. 이를 Queue를 사용함으로 O(n) 으로 품.

https://www.acmicpc.net/problem/21737

3. 18808 스티커 붙이기
- 풀이 : 회전을 어떻게 구현하는지가 핵심.

핵심코드>
pulblic int[][] rotate(int[][] map,int row,int col){
  int[][] temp = new int[col][row];
  for(int i=0;i<col;++i)
    for(int j=0;j<row;++j)
      temp[i][j] = map[row-1-j][i]
  return temp;
}

https://www.acmicpc.net/problem/18808
