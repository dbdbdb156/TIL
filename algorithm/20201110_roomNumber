# 백준 1082

// 풀이 방법 : 최대 길이에서 1차적으로 걸러낸 후, 높은수가 많은것부터 출력예정
#define _CRT_SECURE_NO_WARNINGS
#include <cstdio>

// weight 만큼 각값을 몇개 가지고있는지 반환하는 배열
// 각 weight 에 쌓여있는 값의 최대 길이
// 최대 길이에서 1차적으로 값을 걸러낼꺼임
int n, w;
int v[10];
char value[51];
int length;

int main(void) {

	int i;
	scanf("%d", &n);
	for (i = 0; i < n; ++i)
		scanf("%d", &v[i]);
	scanf("%d", &w);

	int min=0;
	for (i = 1; i < n; ++i) {
		if (v[min] > v[i]) {
			min = i;
		}
	}
	length = 0;
	for (; w >= v[min];) {
		value[length++] = '0'+min;
		w -= v[min];
	}
	bool possible=false;
	for (int j = 0; j < length;) {

		for (i = n - 1; i >= 0; --i) {
			// min 이 9이고 i 가 8인경우에 에러가 뜬다.
			if (v[i] <= w + v[min] && min < i) {
				value[j++] = '0' + i;
				w -= v[i];
				w += v[min];
				possible = true;
				break;
			}
		}
		// 아무것도 통과 못했다.
		if (!possible) { 
			if (value[0] == '0')
			{
				value[--length]='\0';
				w += v[min];
				continue;
			}
			break;
		}
		possible = false;

	}
	if (!possible && length <= 0) value[0] = '0';

	printf("%s", value);

	return 0;
}

-------------------------------------------------------
** 문제점 :
- 문제에 대한 핵심은 잡았지만 어떻게 사용할지를 몰랐음.ex) 풀이 방법 : 최대 길이에서 1차적으로 걸러낸 후, 높은수가 많은것부터 출력예정
-> 최대 길이의 문자열을 만든후, 높은수 순서대로 변경시키기

## 아이디어를 구체화 못시키면 문제를 못품.
1. 문제를 어떻게 풀지 방향잡기 **** 핵심
2. 사용할 로직
3. 사용할 자료구조 -> 고급 자료구조라고 마냥 좋은것은 아님.
: 물론 문제에 따라 다르다

* 에러 :
- min 이 9이고 i 가 8인 경우를 처리 못함.


