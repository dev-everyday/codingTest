# 문제
본 문제의 저작권은 (주)브랜치앤바운드에 있으며, 저작자의 동의 없이 무단 전재/복제/배포를 금지합니다.
링크 참고해주시기 바랍니다.

# 풀이
오름차순으로 배열이 주어지기 때문에 min_space 를 갱신하면서 min_cnt를 세어주면 되는 문제다.

# 코드
```
#include<iostream>
#include<algorithm>
using namespace std;
int village[1010];

int main(int argc, char** argv)
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    int n;
    cin >> n;
    int min_space = 1000100;
    int min_cnt = 0;
    cin >> village[0];
    for(int i=1;i<n;i++){
        cin >> village[i];
        if(village[i]-village[i-1]<min_space){
            min_space = village[i]-village[i-1];
            min_cnt=1;
        } else if (village[i]-village[i-1]==min_space){
            min_cnt++;
        }
    }
    cout << min_cnt;
    return 0;
}
```