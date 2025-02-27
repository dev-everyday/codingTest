# 문제

회사에는 N개의 회의실이 있다. 수많은 팀이 모여 토론하고 업무를 처리하기 위해서는 회의실이 필수적이다.

내부망에 아주 간단한 회의실 예약 시스템이 있지만 편의성이 매우 떨어진다. 단순히 예약된 회의의 목록만 표시되기 때문에, 방 별로 비어 있는 시간이 언제인지를 확인하기가 힘든 것이다. 당신은 이를 직접 해결해 보기로 마음 먹었다.

회의실 이용 규칙은 다음과 같다:

- 회의실은 9시부터 18시까지만 사용 가능하다. 모든 회의의 시간은 이 안에 완전히 포함되어야 한다.

- 회의는 정확히 한 회의실을 연속한 일정 시간 동안만 점유한다. 즉 각 회의는 (회의실, 시작 시각, 종료 시각)의 정보로 나타낼 수 있다.

- 회의의 시작과 종료 시각은 시(時, hour) 단위로만 설정 가능하다. 같은 회의실을 사용하는 회의 시간은 서로 겹칠 수 없다. 여기서 겹친다는 것은, 두 회의 모두에 포함되는 시간이 1시간 이상 존재한다는 것을 의미한다. 예를 들어, 10시-12시의 회의와 11시-13시의 회의는 겹치는데, 11시-12시의 시간이 두 회의 모두에 포함되기 때문이다.

- 한 회의가 끝나는 시각에, 같은 회의실에서 다른 회의가 시작하는 것은 허용된다. 이 경우 두 회의가 겹치지 않기 때문이다.

- 길이가 0인 회의, 즉 시작 시각과 종료 시각이 동일한 회의는 예약된 바 없으며, 새롭게 잡을 수도 없다.

 

이미 예약된 M개의 회의에 대한 정보가 주어지면, 회의실별로 비어 있는 시간대를 정리해 출력하는 프로그램을 작성해 보자. 구체적인 형식은 아래를 참고하시오.

# 풀이

우선 unordered_map을 사용하였는데 key로 string으로 설정하고 array<int,24>를 key로 설정해주었다.

이름을 입력받아서 그 이름을 index로 가지고 hours는 24개 모두 0으로 초기화된 array를 가지고 있게 설정하였다.

for문을 돌 때 const auto&를 사용하였는데 정리하면 아래와 같다.

1) 속도 & 메모리 최적화가 필요하면 → const auto& entry

2) 값을 변경해야 하면 → auto& entry

3) 초보자가 가독성을 높이고 싶다면 → const pair<string, array<int, 24>>& entry

4) 간단하지만 비효율적인 방식(복사가 일어나서) → auto entry

중간에 오름차순 정렬이 필요하다는 사실과 -----이 마지막 index에는 출력하지 않아야해서 아래와 같이 바꿔주었다.

unordered_map을 map으로 변경하면서 순서가 생기고 자동으로 오름차순으로 정렬이 된다.

for (auto it = data.begin(); it != data.end(); ++it) 

반복자는 주소를 가리키는 포인터와 같은 개념이라 const auto&로 선언하면 반복자의 이동이 불가능해서 auto it로 선언한다.

반복자는 변경이 가능한 객체여야 하므로 const auto it로 선언하였다.

std::next(it)의 역할은 it(반복자)의 다음 위치를 반환하는 함수이고 원본을 변경하지 않고 새로운 반복자를 반환할 수 있다.

그래서 it++할 필요 없이 next(it) != data.end()로 해당 값이 마지막 index인지 확인할 수 있다.

# 코드
```
#include <iostream>
#include <string>
#include <map>
#include <array>
#include <vector>
#include <utility>
using namespace std;

int n, m;

int main() {
    scanf("%d %d", &n, &m);
    map<string, array<int, 10>> data;
    string name;

    for (int i = 0; i < n; i++) {
        cin >> name;
        array<int, 10> hours = {0};
        data[name] = hours;
    }

    int st, et;
    for (int i = 0; i < m; i++) {
        cin >> name >> st >> et;
        for (int j = st; j < et; j++) {  
            data[name][j - 9] = 1;
        }
    }

    for (auto it = data.begin(); it != data.end(); ++it) {
        cout << "Room " << it->first << ":"<<endl;
        vector<pair<int, int>> empty_rooms;
        int cur_idx = -1;

        for (int j = 0; j < 10; j++) {
            if (it->second[j] == 0) {
                if (cur_idx == -1) {
                    cur_idx = j;  
                }
            } else {
                if (cur_idx != -1) {
                    empty_rooms.push_back({cur_idx, j});
                    cur_idx = -1;
                }
            }
        }
        if (cur_idx != -1 && cur_idx != 9) {
            empty_rooms.push_back({cur_idx, 9});
        }

        if (empty_rooms.empty()) {
            cout << "Not available" << endl;
        } else {
            cout << empty_rooms.size() << " available:" << endl;
            for (const auto& entry : empty_rooms) {
                if(entry.first<1){
                    cout << "0"<< entry.first + 9 << "-" << entry.second + 9 << endl;
                }else{
                    cout << entry.first + 9 << "-" << entry.second + 9 << endl;
                }
            }
        }

        if (next(it) != data.end()) {
            cout << "-----" << endl;
        }
    }

    return 0;
}
```
```
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        
        int n = Integer.parseInt(st.nextToken());
        int m = Integer.parseInt(st.nextToken()); 

        Map<String, int[]> data = new TreeMap<>();

        for (int i = 0; i < n; i++) {
            String name = br.readLine();
            data.put(name, new int[10]);
        }

        for (int i = 0; i < m; i++) {
            st = new StringTokenizer(br.readLine());
            String name = st.nextToken();
            int stTime = Integer.parseInt(st.nextToken());
            int etTime = Integer.parseInt(st.nextToken());

            int[] hours = data.get(name);
            for (int j = stTime; j < etTime; j++) {
                hours[j - 9] = 1; 
            }
        }

        StringBuilder sb = new StringBuilder();
        Iterator<Map.Entry<String, int[]>> iterator = data.entrySet().iterator();
        while (iterator.hasNext()) {
            Map.Entry<String, int[]> entry = iterator.next();
            String roomName = entry.getKey();
            int[] hours = entry.getValue();

            sb.append("Room ").append(roomName).append(":\n");

            List<int[]> emptyRooms = new ArrayList<>();
            int curIdx = -1;

            for (int j = 0; j < 10; j++) {
                if (hours[j] == 0) {
                    if (curIdx == -1) {
                        curIdx = j;
                    }
                } else {
                    if (curIdx != -1) {
                        emptyRooms.add(new int[]{curIdx, j});
                        curIdx = -1;
                    }
                }
            }
            if (curIdx != -1 && curIdx != 9) {
                emptyRooms.add(new int[]{curIdx, 9});
            }

            if (emptyRooms.isEmpty()) {
                sb.append("Not available\n");
            } else {
                sb.append(emptyRooms.size()).append(" available:\n");
                for (int[] interval : emptyRooms) {
                    if (interval[0] < 1) {
                        sb.append(String.format("0%d-%d\n", interval[0] + 9, interval[1] + 9));
                    } else {
                        sb.append(String.format("%d-%d\n", interval[0] + 9, interval[1] + 9));
                    }
                }
            }

            if (iterator.hasNext()) {
                sb.append("-----\n");
            }
        }

        System.out.print(sb.toString());
    }
}

```