# 알고리즘
## BFS & BACKTRACING
### 백준 14502 연구소
#### 풀이 : 모든 경우의 수의 벽을 세운 후에 bfs 각기 실행.

#### 어려움 
- 현상 : 다른 벽들을 세우고 bfs 각자 실행하는 과정에서 의도했던 최소값보다 더 작은 값이 나옴.
1) bfs 내의 문제였나 디버깅 해봄. 예시 하나를 실행해봄으로서 문제 없이 답이 나옴을 알았음
2) 전역변수로 선언했던 queue 객체가 힙 영역에 쌓여서 의도치 않게 연산 과정에서 잘못된 주소값 참조가 된것은 아닌가 점검했지만 문제 없었음

* 해답 : 문제 내에서 bfs 를 실행하기전 3가지 벽의 위치를 찾는데 원래 세워져있던 벽들도 함께 선택을 했음
설계를 할때는 3개를 뽑았는줄 알았지만, 사실은 3가지 벽, 2가지벽+중복된 벽 1개, 1가지벽+중복된 벽 2개, 중복된벽 3가지도 중복이 되서 계산이 됬기에
의도하지 않은 값이 나옴.
-> 예외처기를 신중하게 해야함.

https://www.acmicpc.net/problem/14502



package bj_14502;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.LinkedList;
import java.util.Queue;
import java.util.StringTokenizer;

// 스택,큐는 
public class Main {
	public static int [][]map;
	public static int zero,row,col;
	public static boolean mark[][];
	public static Queue<node> two;
	
	public static void main(String args[]) throws IOException{
		
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		
		StringTokenizer st = new StringTokenizer(br.readLine());
		row = Integer.parseInt(st.nextToken());
		col = Integer.parseInt(st.nextToken());
		
		map = new int[row][col];
		mark = new boolean[row][col];
		
		two = new LinkedList<node>();
		
		zero = 0;
		for(int i=0;i<row;++i) {
			st = new StringTokenizer(br.readLine());
			for(int j=0;j<col;++j) {
				int temp = Integer.parseInt(st.nextToken());
				map[i][j] = temp;
				if(temp == 2){
					two.add(new node(i,j));
				}
				else if(temp == 0) {
					zero++;
				}
			}
			Arrays.fill(mark[i],false);
		}
			
		int min = row*col+1;
		for(int i=0;i<row*col;++i){
			for(int j=i+1;j<row*col;++j) {
				for(int k=j+1;k<row*col;++k) {
					if(map[i/col][i%col] == 0 && map[j/col][j%col] == 0 && map[k/col][k%col] == 0) {
						map[i/col][i%col] = 1;
						map[j/col][j%col] = 1;
						map[k/col][k%col] = 1;
						min = Math.min(min, bfs(two));
						map[i/col][i%col] = 0;
						map[j/col][j%col] = 0;
						map[k/col][k%col] = 0;
						for(int w=0;w<row;++w)
							Arrays.fill(mark[w],false);
					}
				}
			}
		}

		System.out.println(zero-min);
		
	}
	public static int bfs(Queue<node> two) {
		
		int cnt = 3;
		int []gor = {1,0,-1,0};
		int []goc = {0,1,0,-1};
		
		Queue<node> q = new LinkedList<node>();
		q.addAll(two);
		
		while(!q.isEmpty()) {
			int r = q.peek().getrow();
			int c = q.peek().getcol();
			if(!mark[r][c]&&map[r][c]==2) {
				mark[r][c] =true;
			}
			q.poll();
			for(int i=0;i<4;++i) {
				int nr = r + gor[i];
				int nc = c + goc[i];
				if(nr >=0 && nr<row && nc >= 0 && nc<col) {
					if(map[nr][nc]==0 && !mark[nr][nc]) {
						cnt++;
						mark[nr][nc] = true;
						q.add(new node(nr,nc));
					}
					
				}
				
			}
		}
		
		
		return cnt;
	}
	
	
}
class node{
	private int row;
	private int col;
	public node(int row,int col) {
		this.row = row;
		this.col = col;
	}
	public int getrow() {
		return this.row;
	}
	public int getcol() {
		return this.col;
	}
}

----------------------------
#### 문제 풀며 추가 궁금증 해결 :  java 의 깊은 복사와 얕은 복사.
: JVM 내의 heap 영역에 객체가 생성되고, 그 객체를 다른 변수가 참조하게 되며, 의도치않은 값의 변화로 인한 논리 오류 발생
, 깊은 복사와 얕은 복사에 대해서, 알게 되었고 Clonable 클래스를 implements 함으로 .clone 함수 사용이 가능함을 암.


