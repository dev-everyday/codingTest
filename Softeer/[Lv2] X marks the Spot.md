# 문제

연탄을 모든 집에 배달하려고 했던 산타는 큰 고민에 빠집니다. 각 집에는 연탄 난로가 있는데, 난로와 연탄 모두 원 모양으로 되어있기 때문에 난로의 반지름의 길이가 연탄의 반지름의 길이의 배수인 집에서만 이 연탄을 사용할 수 있다는 것입니다.
n개의 집에 각각 놓여 있는 난로의 반지름의 길이가 주어졌을 때, 산타는 연탄의 반지름의 길이를 처음에 잘 설정하여 최대한 많은 집에서 이 연탄을 사용할 수 있도록 만들고자 합니다. 산타를 도와 연탄이 사용가능한 집의 수를 최대로 하는 프로그램을 작성해보세요. 단, 난로의 반지름과 연탄의 반지름은 항상 정수로 나타내지며, 연탄의 반지름은 항상 1보다 커야만 함에 유의합니다.
퍼즐을 좋아하는 하이비는 작년에 이어 올해에도 퍼즐과 관련된 문제를 내기로 했다.
이번에는 Indirect Indexing으로, 다음과 같은 방식을 따른다.
1. N개의 문자열 쌍 (S1,T1), (S2,T2),…, (SN,TN)이 주어진다. 각 쌍에 대해, Si의 길이와 Ti의 길이는 같다.
2.  Si에서 글자 x 또는 X가 등장하는 위치를 Pi라고 하자. 이 위치는 항상 유일하다.
3. 이때, Ti의 Pi번째 글자를 읽으면 된다. 단, 소문자는 대문자로 바꿔야 한다.
4. 예를 들어, Si가 Indexing이고 Ti가 Indirect라면 읽게 되는 글자는 R이 된다

# 풀이

간단하게 A 문자열에 x나 X 위치에 해당하는 문자를 B에서 찾아서 n개를 이어서 String으로 만드는 것이다.﻿
algorithm 헤더 파일을 추가하고 string에 append할 때 toupper를 이용해서 대문자로 더해주기만 하면 된다.

# 코드
```
#include<iostream>
#include<string>
#include<algorithm>
using namespace std;

int main(int argc, char** argv)
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    int n;
    cin >> n;
    string a, b, ans;
    for(int i=0;i<n;i++){
        cin >> a >>b;
    for(int i=0;i<a.length();i++){
        if(a[i]=='x'||a[i]=='X'){
            ans+=toupper(b[i]);
        }
    }
    }
    cout<<ans;
    return 0;
}
```