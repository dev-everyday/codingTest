# 문제
루팡은 배낭을 하나 메고 은행금고에 들어왔다. 금고 안에는 값비싼 금, 은, 백금 등의 귀금속 덩어리가 잔뜩 들어있다. 배낭은 W ㎏까지 담을 수 있다.
각 금속의 무게와 무게당 가격이 주어졌을 때 배낭을 채울 수 있는 가장 값비싼 가격은 얼마인가?
루팡은 전동톱을 가지고 있으며 귀금속은 톱으로 자르면 잘려진 부분의 무게만큼 가치를 가진다.

# 풀이
먼저 총 무게 W가 있고 W가 0이 될때까지 담을 수 있다.
먼저 vector pair로 각각 무게와 무게당 가격을 담아준다.
sort를 통해서 무게가 무거운 순으로 정렬하는데 이 때 compare 함수로 second에 담긴 값이 큰 순으로 정렬해준다.
이후에 vector를 돌면서 w가 v[i].first보다 더 많이 남으면 무게만큼 다 담고 w만큼만 담을 수 있으면 w만 담아주면 된다.

# 코드
```
#include <iostream>
#include <algorithm>
#include <utility>
#include <vector>
using namespace std;
bool compare(pair<int,int>a, pair<int,int>b){
    return a.second>b.second;
}
int main(int argc, char** argv)
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    int w, n, m, p;
    cin >>w>>n;
    vector<pair<int,int>>v(n);
    for(int i=0;i<n;i++){
        cin >> v[i].first>>v[i].second;
    }
    sort(v.begin(), v.end(), compare);
    int ans = 0;
    for(int i=0;i<n;i++){
        if(w==0)break;
        if(v[i].first<=w){
            ans+=v[i].first*v[i].second;
            w-=v[i].first;
        } else{
            ans+=w*v[i].second;
            w=0;
        }
    }
    cout<<ans;
    return 0;
}
```