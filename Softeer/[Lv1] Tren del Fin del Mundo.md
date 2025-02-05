# 문제
Southern Fuegian Railway는 세상에서 가장 남쪽에 있는 철도이다.
Southern Fuegian Railway는 x축의 양의 방향을 동쪽으로 하는 2차원 좌표평면으로 나타내어진다.
Southern Fuegian Railway는 N개의 역과 역 사이를 잇는 N−1개의 철로로 구성되어 있다. i번째 역은 (xi,yi)에 있으며, j번째 철로는 j번 역과 j+1번 역 사이를 잇는 선분이다. (1 ≤ i ≤ N; 1 ≤ j ≤ N−1) 
Southern Fuegian Railway를 보러 간 선아는 세상에서 가장 남쪽에 있는 철도가 지나는 가장 남쪽 점이 어디일지 궁금해졌다.

# 풀이
간단하다.
간단히 y 의 값이 최소가 되는 (x, y)를 찾아 출력하면 된다.

# 코드
```
#include<iostream>
using namespace std;

int main(int argc, char** argv)
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    int n, x, y;
    cin >> n;
    int ans_x = 0, ans_y=1001;
    for(int i=0;i<n;i++){
        cin >> x >> y;
        if(y<ans_y){
            ans_y=y;
            ans_x=x;
        }
    }
    cout << ans_x<<" "<<ans_y;
    return 0;
}
```