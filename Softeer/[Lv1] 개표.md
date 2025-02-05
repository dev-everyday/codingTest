# 문제
투표가 끝난 뒤에는 개표를 해야 한다. 일반적으로 개표는 칠판을 사용하며, 한 표가 나올 때마다 한 획을 추가로 긋는 방식을 사용한다.
이 문제에서는 다음과 같은 방식으로 개표를 진행한다.
- 모든 후보자는 0표, 즉 아무것도 그려져 있지 않는 상태로 시작한다.
- 어떤 후보자가 한 표를 받을 때마다, |를 맨 뒤에 그린다.
- 단, 그 후보자가 5표를 받을 때마다, |를 그리는 대신 이미 있던 4개의 |에 가로줄을 그어 ++++를 만든다. 이후 1칸의 공백을 뒤에 추가한다.
예를 들면, 12표를 받은 후보의 경우 칠판에는 ++++ ++++ ||가 적히게 된다.

# 풀이
간단하게 5로 나눈 몫과 나머지를 구해서 ++++ 혹은 | 로 나타내면 되는 문제이다.

# 코드
```
#include<iostream>
using namespace std;

int main(int argc, char** argv)
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    int T, n;
    cin >> T;
    for(int i=0;i<T;i++){
        cin >> n;
        int quiot=n/5, remain=n%5;
        while(quiot>0){
            cout << "++++";
            quiot--;
            if(quiot>0 || remain >0){
                cout << " ";
            }
        }
        while(remain){
            cout << "|";
            remain--;
        }
        cout<<endl;
    }
    return 0;
}
```