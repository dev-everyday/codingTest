# 문제

N-Queen 문제는 크기가 N × N인 체스판 위에 퀸 N개를 서로 공격할 수 없게 놓는 문제이다.

N이 주어졌을 때, 퀸을 놓는 방법의 수를 구하는 프로그램을 작성하시오.

# 입력

첫째 줄에 N이 주어진다. (1 ≤ N < 15)

# 출력

첫째 줄에 퀸 N개를 서로 공격할 수 없게 놓는 경우의 수를 출력한다.

# 풀이

간단하게 브루트포스 알고리즘을 이용해서 풀 수 있다.

배열의 너비와 현재 row를 가지는 함수를 만들고 해당 배열에 놓을 수 있는지 여부를 판단하고 놓을 수 있다면 현재 row가 n인지 확인한다.

만약 현재 row가 n이라면 ans++을 해주고 row가 n이 아니라면 다음 row+1을 인자로 가지는 재귀로 구현한다.

또한 board[row][i]에 queen을 놓았는지 여부를 체크해준다(=visited 배열 역할)

해당 row에 놓을 수 있는지 여부는 possible 함수로 판단하는데 다른 row에 해당 column과 동일한 곳에 queen이 있거나 대각선에 있는지 여부를 판단하는 코드이다.

# 코드

```
#include <iostream>
using namespace std;
int board[16][16];
int n, ans;

int possible(int x, int y) {
	for (int i = 1; i <= n; i++) {
		if (i != x && board[i][y]) {
			return 0;
		}
	}
	for (int i = 1; i <= n; i++) {
		if (x - i > 0) {
			if ((y - i >= 1 && board[x - i][y - i] == 1)) {
				return 0;
			}
			if (y + i <= n && board[x - i][y + i] == 1) {
				return 0;
			}
		}
	}
	return 1;
}

void queen_never_cry(int n, int row) {
	for (int i = 1; i <= n; i++) {
		if (possible(row, i)) {
			board[row][i] = 1;
			if (n == row) {
				ans++;
			} else{
				queen_never_cry(n, row + 1);
			}
			board[row][i] = 0;
		}
	}
	return;
}

int main() {
	ios::sync_with_stdio(false);
	cin.tie(0);
	cin >> n;
	// 배열 너비 n, 현재 row
		queen_never_cry(n, 1);
	cout << ans;
	return 0;
}
```