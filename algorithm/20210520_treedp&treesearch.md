# 알고리즘
## TREE DP & pre,in,post order
### 백준

1. 4256 트리
- 풀이 : 프리오더, 인오더의 값을 알면 post 오더의 값을 알수 있다.
특징 )
-preorder : 가장 첫번째 노드 = root
-inorder  : 중간 노드를 기준으로 left subtree 와 right subtree 가 나뉨
-postorder : 가장 나중 노드가 = root
이를 통해서, root 를 preorder를 통해서 찾고, inorder 를 기준으로 재귀 분할정복
+ root 참조는 preorder 의 루트 바로옆 노드와, left subtree의 길이를 파악 후 그 left subtree의 root 보다 길이만큼 이동하면 됨.

핵심코드>
public static void maketree(int root,int left,int right) {
		
		if(left>right) return ;
		int index =0;
		for(int i=0;i<right;++i)
			if(preorder[root]==inorder[i]) {
				index = i;
				break;
			}
		maketree(root+1,left,index-1);
		maketree(root+1+(index-left),index+1,right);
		sb.append(preorder[root]).append(" ");
	}
  
  2. 1949 우수 마을
  - 트리 DP
  - 풀이)
  DP 배열에 어떤것을 저장할까가 중요.
  - TOP 다운 방식으로 DP 에 저장을 함.
  ** DP 에 함수를 가면서 저장하는것이 아닌, DP 에 들어갈 값들을 구한다음에 현재의 DP 의 값에 참조해서 값을 구하는 형식
  - 트리 DP 에서 DP 는 어떤 값을 추가할지가 핵심
  
  핵심코드>
  public static void dfs(int index) {
		
		visited[index] = true;
		dp[index][0] = 0;
		dp[index][1] = city[index]; 
		
		ArrayList<Integer> v = list.get(index);
		for(int i=0;i<v.size();++i) {
			if(!visited[v.get(i)]) {
				dfs(v.get(i));
				
				dp[index][0] += Math.max(dp[v.get(i)][0],dp[v.get(i)][1]);
				dp[index][1] += dp[v.get(i)][0];
			}
		}
		
		
	}
  
