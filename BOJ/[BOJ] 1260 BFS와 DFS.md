# 문제

그래프를 DFS로 탐색한 결과와 BFS로 탐색한 결과를 출력하는 프로그램을 작성하시오. 단, 방문할 수 있는 정점이 여러 개인 경우에는 정점 번호가 작은 것을 먼저 방문하고, 더 이상 방문할 수 있는 점이 없는 경우 종료한다. 정점 번호는 1번부터 N번까지이다.

# 입력

첫째 줄에 정점의 개수 N(1 ≤ N ≤ 1,000), 간선의 개수 M(1 ≤ M ≤ 10,000), 탐색을 시작할 정점의 번호 V가 주어진다. 다음 M개의 줄에는 간선이 연결하는 두 정점의 번호가 주어진다. 어떤 두 정점 사이에 여러 개의 간선이 있을 수 있다. 입력으로 주어지는 간선은 양방향이다.

# 출력

첫째 줄에 DFS를 수행한 결과를, 그 다음 줄에는 BFS를 수행한 결과를 출력한다. V부터 방문된 점을 순서대로 출력하면 된다.

# 풀이

순서대로 DFS와 BFS를 구현하였다.

visited 배열을 선언하여 해당 노드에 방문 여부를 체크하였고 resetVisited를 통해서 BFS에서 재사용 시 초기화를 하는 함수를 선언하였다.

dfs의 경우에는 당장 graph[node]에서 방문하지 않은 노드가 있다면 바로 방문하도록 하였고 bfs의 경우에는 queue를 통해서 바로 방문하는 것이 아니라 queue에 넣은 순서대로 방문하도록 하였다.

또한 graph 방문 순서가 node 숫자가 작은 순이기 때문에 sort를 해주는 것을 잊지말도록 하자.

# 코드
```
#include <iostream>
#include <algorithm>
#include <vector>
#include <queue>
using namespace std;

vector<int> graph[1010];
bool visited[1010];

void resetVisited(int n) {
    for (int i = 1; i <= n; i++) {
        visited[i] = false;
    }
}

void dfs(int node) {
    cout << node << " ";
    for (int neighbor : graph[node]) {
        if (!visited[neighbor]) {
            visited[neighbor] = true;
            dfs(neighbor);
        }
    }
}

void bfs(int start) {
    queue<int> q;
    q.push(start);
    visited[start] = true;

    while (!q.empty()) {
        int node = q.front();
        q.pop();
        cout << node << " ";
        for (int neighbor : graph[node]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(0);

    int n, m, startNode;
    cin >> n >> m >> startNode;

    for (int i = 0; i < m; i++) {
        int start, end;
        cin >> start >> end;
        graph[start].push_back(end);
        graph[end].push_back(start);
    }

    for (int i = 1; i <= n; i++) {
        sort(graph[i].begin(), graph[i].end());
    }

    resetVisited(n);
    visited[startNode] = true;
    dfs(startNode);
    cout << "\n";

    resetVisited(n);
    bfs(startNode);
    cout << "\n";

    return 0;
}
```