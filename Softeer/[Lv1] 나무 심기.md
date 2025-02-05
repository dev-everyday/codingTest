# 문제
남우는 나무를 2개 심으려고 합니다. 나무는 주어진 n개의 위치 중 서로 다른 두 곳에 꼭 심어야만 하며, 1번 위치부터 n번 위치까지 각 위치마다 토양의 비옥함에 해당하는 값 Fi가 주어졌을 때 남우는 나무가 심어지는 두 위치 a, b에서 토양의 비옥함의 곱인 Fa ∗ Fb가 최대가 되도록 나무를 심으려고 합니다. 남우가 적절한 위치에 나무를 심을 수 있도록 하는 프로그램을 작성해보세요.
만약 n이 3이고 다음과 같이 토양의 비옥함이 순서대로 5, -1, 4인 경우 5, 4 위치에 나무를 심으면 비옥함의 곱이 20으로 최대가 됩니다.

# 풀이
우선 음수도 포함되어있기 때문에 정렬을 해준 후에 음수 간 곱과 양수 간 곱을 비교하여 최고 값을 구하였다.

# 코드
```
#include <iostream>
#include <algorithm>
using namespace std;

int ground[101];
int main(void)
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    int n;
    cin >> n;
    for(int i=0;i<n;i++){
        cin >> ground[i];
    }
    sort(ground, ground+n);
    int a = ground[0]*ground[1];
    int b = ground[n-1]*ground[n-2];
    cout << max(a, b);
    
    return 0;
}
```