
# 문제

자율주행팀 SW 엔지니어인 당신에게 장애물과 도로를 인식할 수 있는 프로그램을 만들라는 업무가 주어졌다.
[그림 1] 지도 예시
우선 [그림 1]과 같이 정사각형 모양의 지도가 있다. 1은 장애물이 있는 곳을, 0은 도로가 있는 곳을 나타낸다.
당신은 이 지도를 가지고 연결된 장애물들의 모임인 블록을 정의하고, 불록에 번호를 붙이려 한다. 여기서 연결되었다는 것은 어떤 장애물이 좌우, 혹은 아래위로 붙어 있는 경우를 말한다. 대각선 상에 장애물이 있는 경우는 연결된 것이 아니다.
[그림 2] 블록 별 번호 부여
[그림 2]는 [그림 1]을 블록 별로 번호를 붙인 것이다.
지도를 입력하여 장애물 블록수를 출력하고, 각 블록에 속하는 장애물의 수를 오름차순으로 정렬하여 출력하는 프로그램을 작성하시오.

# 풀이

BFS로 구현해주면 된다. 가끔 LV의 단계에 대해서 같은 2레벨인가 싶기도 하다.
백준 아파트 문제 유형과 똑같은데 방문했는지와 장애물이 있다면 queue를 넣어서 시작하고 queue가 빌 때까지 상하좌우로 이동하면서 아파트 개수를 세면 된다.
그리고 마지막으로 정렬을 통해서 장애물 총 개수와 각 몇 개인지 출력해주면 된다.

# 코드
```
#include<iostream>
#include<queue>
#include<vector>
#include<algorithm>
using namespace std;
int arr[26][26], visited[26][26];
int dx[4]={0,0,1,-1};
int dy[4]={1,-1,0,0};
vector<int>ans;
int n;

int bfs(int x, int y){
    visited[x][y]=1;
    queue<pair<int,int>>q;
    q.push({x,y});
    int cnt = 0;
    while(!q.empty()){
        cnt++;
        int x = q.front().first;
        int y = q.front().second;
        q.pop();
        for(int i=0;i<4;i++){
            int next_x=x+dx[i];
            int next_y=y+dy[i];
            if(next_x<0||next_y<0||next_x>=n||next_y>=n){
                continue;
            } else if(visited[next_x][next_y]==0&&arr[next_x][next_y]==1){
                q.push({next_x, next_y});
                visited[next_x][next_y]=1;
            }
        }
    }
    return cnt;
}

int main(int argc, char** argv)
{
    scanf("%d",&n);
    for(int i=0;i<n;i++){
        for(int j=0;j<n;j++){
            scanf("%1d",&arr[i][j]);
        }
    }
    for(int i=0;i<n;i++){
        for(int j=0;j<n;j++){
            if(visited[i][j]==0&&arr[i][j]==1){
                ans.push_back(bfs(i,j));
            }
        }
    }
    sort(ans.begin(), ans.end());
    printf("%d\n",ans.size());
    for(int i:ans){
        printf("%d\n", i);
    }
    return 0;
}
```
```
import java.io.*;
import java.util.*;

public class Main {
    static int[][] arr, visited;
    static int n;
    static int[] dx = {0, 0, 1, -1};
    static int[] dy = {1, -1, 0, 0};
    static List<Integer> ans = new ArrayList<>();

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        arr = new int[n][n];
        visited = new int[n][n];

        for (int i = 0; i < n; i++) {
            String line = br.readLine();
            for (int j = 0; j < n; j++) {
                arr[i][j] = line.charAt(j) - '0';
            }
        }

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (visited[i][j] == 0 && arr[i][j] == 1) {
                    ans.add(bfs(i, j));
                }
            }
        }

        Collections.sort(ans);
        System.out.println(ans.size());
        for (int count : ans) {
            System.out.println(count);
        }
    }

    public static int bfs(int x, int y) {
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{x, y});
        visited[x][y] = 1;
        int count = 0;

        while (!queue.isEmpty()) {
            count++;
            int[] current = queue.poll();
            int curX = current[0], curY = current[1];

            for (int i = 0; i < 4; i++) {
                int nextX = curX + dx[i];
                int nextY = curY + dy[i];

                if (nextX >= 0 && nextY >= 0 && nextX < n && nextY < n) {
                    if (visited[nextX][nextY] == 0 && arr[nextX][nextY] == 1) {
                        queue.offer(new int[]{nextX, nextY});
                        visited[nextX][nextY] = 1;
                    }
                }
            }
        }
        return count;
    }
}
```