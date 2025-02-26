# 문제

글로벌 비즈니스 센터(GBC, Global Business Center)는 현대자동차그룹 통합 사옥이다.

지하 7층, 지상 105층, 높이 약 570m의 규모로 2026년 하반기에 완공을 목표로 현재 공사 중에 있다.

이러한 초고층 높이의 빌딩에는 초고층 승강기가 들어가야 한다. 엘리베이터 정비공인 광우는 0m 부터 100m까지 일정 구간들의 엘리베이터 속도를 검사하는 업무를 맡게 되었다.

빌딩에서 운영되는 엘리베이터 구간은 N개의 구간으로 나뉘며 해당 구간의 제한 속도이 주어진다. 구간의 총 합은 100m 이며 각 구간별 구간의 길이와 제한 속도 모두 양의 정수로 주어진다.

예를 들어보자. 구간이 3이라고 할 때,

▶ 첫 번째 구간의 길이는 50m 이고 제한 속도는 50m/s

▶ 두 번째 구간의 길이는 40m 이고 제한 속도는 40m/s

▶ 세 번째 구간의 길이는 10m 이고 제한 속도는 30m/s

이 구간에서 제한 속도를 벗어나면(즉 제한속도를 초과하면) 서버에 초과한만큼의 속도가 로그에 남는다. 불행하게도 현재 서버의 상태가 off 상태임으로 광우는 서버의 데이터를 받아볼 수가 없다. 광우는 임의의 구간의 길이와 속도를 정하여 시범운행 할 때, 가장 제한 속도가 크게 벗어난 값을 스스로 구해야 한다.

M개의 구간을 검사한다고 할 때 예를 들면,

▶ 첫 번째 구간의 운행 길이는 60m 이고 속도는 76m/s

▶ 두 번째 구간의 운행 길이는 18m 이고 속도는 28m/s

▶ 세 번째 구간의 운행 길이는 22m 이고 속도는 50m/s이라고 했을 때, 제한 속도를 벗어나 가장 차이가 큰 속도를 구해 보자.

첫번째 구간 50m 까지에서 제한 속도와 실제 운행 속도를 비교했을 때, 제한 속도를 26m/s 초과했다. 이후 두번째 구간과 실 운행한 첫번째 구간이 10m 정도 겹치는데, 이때 제한 속도를 36m/s 초과하게 된다.

그 이후 구간들에서는 차이가 그보다 크지 않으므로 가장 큰 속도 차이는 36m/s임을 알 수 있다.



주어진 구간의 제한속도와 광우가 테스트한 구간의 속도를 기준으로 가장 크게 제한 속도를 넘어간 값이 얼마인지 구해보자.

# 풀이

먼저 limit와 test pair로 범위의 길이와 속도를 저장한다.

범위 문제이기 때문에 각 vector의 개수를 i, j로 따로 가져가게 되었고 100이 보장된다는 하에 pos가 100까지 이동할 때까지를 기준으로 잡았다.

둘 중 작은 범위를 선택해서 이동할 경우 test에서 limit의 속도를 빼고 갱신하였고 둘의 남은 거리를 뺀 후 0이면 각각 다음 범위로 이동하게 하였다.

이게 왜 LV 2일까 내가 바보인걸까 하하.

# 코드
```
#include <iostream>
#include <vector>
#include <algorithm>
#include <utility>

using namespace std;

int main() {
    int n, m;
    cin >> n >> m;

    vector<pair<int,int>> limit(n);
    vector<pair<int,int>> test(m);

    for (int i = 0; i < n; i++) {
        cin >> limit[i].first >> limit[i].second;
    }
    for (int i = 0; i < m; i++) {
        cin >> test[i].first >> test[i].second;
    }

    int max_exceed = 0;
    int i = 0, j = 0;
    int pos = 0;

    while (pos< 100) {
        int min_length = min(limit[i].first, test[j].first);

        int exceed = test[j].second - limit[i].second;
        if (exceed > 0) {
            max_exceed = max(max_exceed, exceed);
        }

        limit[i].first -= min_length;
        test[j].first -= min_length;
        pos += min_length;

        if (limit[i].first == 0) i++;
        if (test[j].first == 0) j++;
    }

    cout << max_exceed << endl;
    return 0;
}
```