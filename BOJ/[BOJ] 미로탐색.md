# 문제

N×M크기의 배열로 표현되는 미로가 있다.
1	0	1	1	1	1
1	0	1	0	1	0
1	0	1	0	1	1
1	1	1	0	1	1
미로에서 1은 이동할 수 있는 칸을 나타내고, 0은 이동할 수 없는 칸을 나타낸다. 이러한 미로가 주어졌을 때, (1, 1)에서 출발하여 (N, M)의 위치로 이동할 때 지나야 하는 최소의 칸 수를 구하는 프로그램을 작성하시오. 한 칸에서 다른 칸으로 이동할 때, 서로 인접한 칸으로만 이동할 수 있다.
위의 예에서는 15칸을 지나야 (N, M)의 위치로 이동할 수 있다. 칸을 셀 때에는 시작 위치와 도착 위치도 포함한다.
입력

첫째 줄에 두 정수 N, M(2 ≤ N, M ≤ 100)이 주어진다. 다음 N개의 줄에는 M개의 정수로 미로가 주어진다. 각각의 수들은 붙어서 입력으로 주어진다.

# 출력

첫째 줄에 지나야 하는 최소의 칸 수를 출력한다. 항상 도착위치로 이동할 수 있는 경우만 입력으로 주어진다.

# 풀이

자꾸 틀렸습니다 가 나와서 의문을 가졌는데 ios::sync_with_stdio(false) 를 사용하고 scanf와 cin을 혼용해서 에러가 발생한 것이었다.

문제를 풀 때 cin과 scanf를 혼용한다면 ios::sync_with_stdio(false) 설정을 꼭 지우도록 하자.

문제 자체는 queue를 사용하여서 BFS로 구현하였다.

hop 배열에 몇 번 이동했는지를 저장하고 이미 이동하였다면 해당 이동값이 최솟값이라는 것이 보장되므로 visited 역할로도 사용하였다.

# 코드

```
#include <iostream>
#include <queue>
using namespace std;

int n, m;
int map[101][101], hop[101][101];
int dx[4] = { 0, 0, -1, 1 };  
int dy[4] = { -1, 1, 0, 0 };
queue<pair<int, int>> q;

int main() {
    cin >> n >> m;

    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            scanf("%1d", &map[i][j]);
        }
    }

    q.push({ 1, 1 });
    hop[1][1] = 1;

    while (!q.empty()) {
        int x = q.front().first, y = q.front().second;
        q.pop();

        for (int i = 0; i < 4; i++) {
            int next_x = x + dx[i];
            int next_y = y + dy[i];

            if (next_x >= 1 && next_y >= 1 && next_x <= n && next_y <= m &&
                map[next_x][next_y] == 1 && hop[next_x][next_y] == 0) {
                hop[next_x][next_y] = hop[x][y] + 1;  
                q.push({ next_x, next_y });
            }
        }
    }

    cout << hop[n][m] << "\n";

    return 0;
}

```