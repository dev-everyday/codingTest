# 문제
N명의 학생들의 성적이 학번순서대로 주어졌다.
학번 구간 [A, B]가 주어졌을 때 이 학생들 성적의 평균을 구하는 프로그램을 작성하라.

# 풀이
문제만 잘 읽어주면 된다.
pow(p, n) 쓰고 싶지만 나눠줘야 해서 while로 풀었다.

# 코드
```
#include<iostream>
#include<math.h>
using namespace std;

int main(int argc, char** argv)
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    long long k, p, n;
    cin >> k >> p >> n;
    while(n--){
        k*=p;
        k%=1000000007;
    }
    cout<<k;
    return 0;
}
```