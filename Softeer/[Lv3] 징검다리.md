# 문제
남북으로 흐르는 개울에 동서로 징검다리가 놓여져 있다.
이 징검다리의 돌은 들쑥날쑥하여 높이가 모두 다르다. 철수는 개울의 서쪽에서 동쪽으로 높이가 점점 높은 돌을 밟으면서 개울을 지나가려고 한다.
돌의 높이가 서쪽의 돌부터 동쪽방향으로 주어졌을 때 철수가 밟을 수 있는 돌의 최대 개수는?

# 풀이
내가 눈이 침침한가 몇 자리수인지 눈이 안 보여서 배열을 잘 못 선언했더니 런타임 에러가 났다.

간단하게 sum 배열 만들어주고 i 부터 j까지 합을 j-i+1로 나눠주면 된다.

대신 %.2f로 두 자리 수까지 출력해주자.

# 코드
```
#include <iostream>
using namespace std;

int score[1010010];
int sum[1010010];

int main() {
    ios::sync_with_stdio(false);
    cin.tie(0);

    int n, k;
    cin >> n >> k;
    
    sum[0] = 0; 
    for (int i = 1; i <= n; i++) {
        cin >> score[i];
        sum[i] = sum[i - 1] + score[i]; 
    }

    int a, b;
    while (k--) {
        cin >> a >> b;
        double result = (double)(sum[b] - sum[a - 1]) / (b - a + 1);
        printf("%.2f\n", result);
    }

    return 0;
}

```