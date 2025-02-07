# 문제
바이러스가 숙주의 몸속에서 1초당 P배씩 증가한다.
처음에 바이러스 K마리가 있었다면 N초 후에는 총 몇 마리의 바이러스로 불어날까? N초 동안 죽는 바이러스는 없다고 가정한다.

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