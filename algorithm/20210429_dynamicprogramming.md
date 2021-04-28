# 알고리즘
## DP
### 백준

####1.2293 동전1
- knapsack 문제와 유사
: 메모라이즈를 통해서 지나왔던 길을 참조
- 애로사항 : 포문의 위치를 바꾸니 중복된 길도 모두다 검색함.
ex) 원했던 값은 10이였지만 값이 128이 나옴.
-> 중복을 제하는 방법 : for 문의 위치를 바꾸면 coin의 값으로 sorting 을 하기에 중복이 제거됨.

핵심코드>

for(int j=0;j<n;++j) {
			for(int i=1;i<=k;++i) {
				if(i>=coin[j]) {
					dp[i]+=dp[i-coin[j]];
					continue;
				}
			}
		}

https://www.acmicpc.net/problem/2293

#### 2. 16637 괄호 추가하기
- 풀이 : 미리 배열에 사칙연산을 한 값을 저장해두고 사용함. 재귀함수를 이용해서 index 를 이용한 값 제어
- 애로사항
1) 문제를 제대로 이해하지 않고 문제를 풀어서 문제를 푸는 시간이 오래걸림.
2) 생각했던 로직에서 다른 로직들도 생각나게 되어 생각이 꼬임
3) 재귀함수의 구성에서 boolean 값을 불필요하게 선언함.
4) calculate(memory[0][0],0); calculate(memory[1][0],1); 두가지 함수 선언을 한 함수로 줄일수 있었는데 추후 개선 필요


코드>
	public static void main(String args[]) throws IOException{
		
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		int N = Integer.parseInt(br.readLine());
		
		lennum = (N/2)+1;
		lenoprand = N/2;
		num = new int[lennum];
		oprand = new char[lenoprand];
		
		memory = new int [2][lennum]; 
		
		char [] temp = br.readLine().toCharArray();
		for(int i=0;i<N;++i) {
			if(i%2==0) num[i/2] = temp[i]-'0';
			else if(temp[i]=='+' || temp[i]=='-' || temp[i]=='*'){
				oprand[i/2] = temp[i];
			}
		}
		memory[0] = num;
		for(int i=0;i<lenoprand;++i) {
				char op = oprand[i];
			switch(op) {
				case '+':
					memory[1][i]=memory[0][i]+memory[0][i+1];
					break;
				case '-':
					memory[1][i]=memory[0][i]-memory[0][i+1];
					break;
				case '*':
					memory[1][i]=memory[0][i]*memory[0][i+1];
					break;
				default:
					break;
			}
		}
		
		for(int i=0;i<2;++i) {
			for(int j=0;j<lennum;++j)
				System.out.print( memory[i][j]+" ");
			System.out.println("");
		}
		
		
		max = -(int)Math.pow(2, 31)+1;
		calculate(memory[0][0],0);
		calculate(memory[1][0],1);
		
		System.out.println(max);
		
		
	}
	// index = 사칙연산 인덱스
	public static void calculate(int value, int index) {
		if(index == lenoprand) {
			System.out.println(value);
			max = Math.max(max, value);
			return ;
		}
		else if(index > lenoprand) return ;
		
		// true 라면 사용 했으므로 , 1개밖에 발전 못함.
			char op = oprand[index];
			int temp = 0;
			switch(op) {
				case '+': temp = value + memory[0][index+1];
					break;
				case '-': temp = value - memory[0][index+1];
					break;
				case '*': temp = value * memory[0][index+1];
					break;
				default:
					break;
			}
			calculate(temp,index+1);
		
		if(index+1<lenoprand) {
			op = oprand[index];
			temp = 0;
			switch(op) {
				case '+': temp = value + memory[1][index+1];
					break;
				case '-': temp = value - memory[1][index+1];
					break;
				case '*': temp = value * memory[1][index+1];
					break;
				default:
					break;
			}
			calculate(temp,index+2);
		}
	}
}

https://www.acmicpc.net/problem/16637
