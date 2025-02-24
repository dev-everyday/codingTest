# 문제
연탄을 모든 집에 배달하려고 했던 산타는 큰 고민에 빠집니다. 각 집에는 연탄 난로가 있는데, 난로와 연탄 모두 원 모양으로 되어있기 때문에 난로의 반지름의 길이가 연탄의 반지름의 길이의 배수인 집에서만 이 연탄을 사용할 수 있다는 것입니다.
n개의 집에 각각 놓여 있는 난로의 반지름의 길이가 주어졌을 때, 산타는 연탄의 반지름의 길이를 처음에 잘 설정하여 최대한 많은 집에서 이 연탄을 사용할 수 있도록 만들고자 합니다. 산타를 도와 연탄이 사용가능한 집의 수를 최대로 하는 프로그램을 작성해보세요. 단, 난로의 반지름과 연탄의 반지름은 항상 정수로 나타내지며, 연탄의 반지름은 항상 1보다 커야만 함에 유의합니다.

# 풀이
n이 101﻿이라서 for문으로 2부터 max 정수까지 돌면서 많이 나눠지는 개수를 구하도록 하였다.

# 코드
```
#include <iostream>
using namespace std;

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n, m;
    cin >> n >> m;
    int rowSum[101] = {0};

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            int t;
            cin >> t;
            rowSum[i] += t;
        }
    }

    for (int q = 0; q < 2; q++) {
        int a, b;
        cin >> a >> b;
        for (int i = a - 1; i < b && i < n; i++) {
            rowSum[i]--;
        }
    }

    int total = 0;
    for (int i = 0; i < n; i++) {
        if (rowSum[i] > 0) {
            total += rowSum[i];
        }
    }

    cout << total;
    return 0;
}
```