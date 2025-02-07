# 문제
N명의 학생들의 성적이 학번순서대로 주어졌다.
학번 구간 [A, B]가 주어졌을 때 이 학생들 성적의 평균을 구하는 프로그램을 작성하라.

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