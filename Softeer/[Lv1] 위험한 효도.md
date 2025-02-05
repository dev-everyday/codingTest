# 문제
남우는 어버이날에 부모님께 선물을 사드리기 위해 게임에 참가하게 되었습니다. 게임 종목은 무궁화 꽃이 피었습니다 입니다.
무궁화 꽃이 피었습니다 게임 룰은 다음과 같습니다.
1) 남우와 술래는 처음에 거리 d 만큼 떨어져 있습니다.
2) 남우는 술래를 향해 뛰어가 술래를 터치하고 다시 출발선으로 돌아와야 합니다.
3) 남우는 술래가 뒤를 돌아보고 있을 때만 움직일 수 있으며, 앞을 바라보고 있을 때는 절대 움직일 수 없습니다.
4) 술래는 처음 a 초간은 뒤를 보고 있고, 그 다음 b 초간은 앞을 보고 있고, 다시 a 초간 뒤를, b 초간 앞을, ... 이 과정을 계속 반복합니다.
5) 남우가 술래를 터치한 직후, 술래의 움직임은 달라집니다. 터치된 직후 처음 b 초간은 뒤를 보고 있고, 그 다음 a 초간은 앞을 보고 있고, 다시 b 초간 뒤를, a 초간 앞을, ... 이 과정을 계속 반복합니다.
6) 술래가 앞, 뒤를 돌아보기 위해 자세를 바꾸는 데 걸리는 시간은 0초라고 가정해도 좋습니다.
7) 남우는 최선을 다해 움직이며, 1초에 거리 1만큼 이동이 가능합니다.

# 풀이
간단하게 생각하면 dist만큼의 시간은 무조건 걸리므로 ans에 2*dist를 더하고 뒤를 돈 시간만큼을 계산해서 더해준다.
먼저 dist를 back으로 나눴을 때 나눠진다면 dist/back -1 만큼 forward 초씩 기다려야하고 dist를 forward로 나눴을 때 나눠진다면 dist/forward -1 만큼 back초씩 기다려야 한다.
반면 나눠지지 않는 다면 한 번 더 더해야하므로 dist/back, dist/forward씩 각각 forward, back초를 기다리면 된다.

# 코드
```
#include<iostream>
using namespace std;

int main(int argc, char** argv)
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    int dist, forward, back;
    cin >>forward>>back>>dist;
    int ans = 2*dist;
    if(dist%back==0){
        ans+=(dist/back-1)*forward;
    } else {
        ans+=(dist/back)*forward;
    }
    if(dist%forward==0){
        ans+=(dist/forward-1)*back;
    } else {
        ans+=(dist/forward)*back;
    }
    cout<<ans;
    return 0;
}
```