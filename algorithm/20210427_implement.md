# 알고리즘
## 구현 implement
1. 10994 별찍기 
- 오류 : char 변수를 선언했을때 변수에 공백(' ')을 넣어주지 않으면 오류가 발생 (예외처리 해주기)
https://www.acmicpc.net/problem/10994


2. 20291 파일 정리
- 애로사항 : 
1) Map 을 구현했는데 Key,value -> String , int 로 구현, key 값을 참고를 하지 못해서 Set을 구현해서 관리했었음.
-> 해결 : Map 내장함수에 Keyset() 이라는 함수가 있었음 , 참고로 TreeMap 은 sort이 되어있기에 유용.
ex) Iterator it = list.keySet().iterator(); 

2) StringBuilder 사용시 긴 문자열을 저장할때 연속적인 .append().append() 가 시간 세이브가 더 됨.
ex) sb.append(s).append(" ").append(list.get(s)).append("\n");

https://www.acmicpc.net/problem/20291


3. 1408 24
- 구현 : 23:59:59 -> 00:00:00 등 상황에 음수를 String으로 변환할때 문제가 있을수 있음.

https://www.acmicpc.net/problem/1408


4. 10825 국영수
- Comparable 인터페이스를 사용해서 구현, 즉 sort 하기전 솔팅의 기준을 만들어주고자 함.
- 애로사항 : 변수가 많기에 변수들을 잘못 비교함. 변수를 잘못 참조하는 실수 하지 않도록 하자 

class node implements Comparable<node>{
	/* 변수 밑  함수 생략 */
	@Override
	public int compareTo(node o) {
		if(this.korean!=o.korean)
			return o.korean-this.korean;
		else{
			if(this.english!=o.english)
				return this.english-o.english;
			else {
				if(this.math!=o.math) 
					return o.math-this.math;
				else {
					return this.name.compareTo(o.name);
				}
			}
		}
	}
}

https://www.acmicpc.net/problem/10825

5. 18511 큰 수 구성하기
- 애로사항 :
1) 잘못된 접근 : N 이 10일때, 답이 0이 나오거나 해야 할줄 알았음 <- 문제를 잘못 이해함.
-> 즉 n 자리 수가 나온다고 해서 2자리수가 답이 아니라 n-1자리의 수가 나올수 있음에 대해서 인지 하지 못함.
: 제일 작은 수 부터 차례대로 비교하여 큰수를 저장 하는 수 밖에 떠오르지 않음.

핵심 코드>
public static void findvalue(int value,int high) {
		
		if(value>n) return;
		if(v<value) {
			v = Math.max(v, value);
		}
		
		for(int i=cnt-1;i>=0;--i) {
			findvalue(10*value+k[i],high+1);
		}
	}


https://www.acmicpc.net/problem/18511

