
# 문제
현대자동차그룹의 연구원인 영호는 자동차의 주행거리를 비교하는 프로그램을 만들고 있다.
두 차량 A와 B의 주행거리가 자연수로 주어졌을 때, 주행거리를 비교해서 어느 차량의 주행거리가 더 큰지 알아보자.

# 풀이
풀이 X

# 코드
```
#include<iostream>
using namespace std;

int main(int argc, char** argv)
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    int a, b;
    cin >> a >> b;
    if(a>b){
        cout << "A";
    } else if (a<b){
        cout <<"B";
    } else{
        cout <<"same";
    }
    return 0;
}
```