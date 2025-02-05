# 문제

당신은 인사팀 직원으로, 각 직원의 근태를 확인하고자 한다.
당신의 회사는 자율출퇴근제를 실시하기 때문에 각 직원이 정확히 몇 시에 출근하는 것은 중요하지 않고, 총 근로 시간이 몇 분인지가 중요하다. 총 근로 시간이 법정근로시간을 초과하지 않아야 하면서, 회사와 직원 사이에 계약한 시간 이상이어야 하기 때문이다.
직원이 하루 동안 근무한 시간은 출근 시각과 퇴근 시각 사이의 시간으로 정의한다. 이 문제에서는 식사 시간 등 근무 외 시간을 근무 시간에서 제외하지 않음에 유의하라.
월요일부터 금요일까지 휴가를 쓰지 않은 직원이 매 요일 언제 출근하고 언제 퇴근했는지가 주어질 때, 이 직원이 5일 동안 총 몇 분을 근무했는지를 구하는 프로그램을 작성하라.

# 풀이

간단하게 10:00 19:00 이 주어졌을 때 문자열을 int로 잘 parsing해서 계산해주면 되는 문제다.
stoi를 사용해서 미리 입력받은 문자열에서 substr을 통해 시와 분을 분리하고 이를 int로 변환한다.
이후에 hour에는 60을 곱하고 minute은 그대로 더해준 다음 마지막에 총 합끼리의 차이를 계산해주자.

# 코드
```
#include<iostream>
#include<string>
using namespace std;

int main(int argc, char** argv)
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    
    string startTime, endTime;
    int startSum = 0, endSum = 0;
    for(int i=0;i<5;i++){
      cin >> startTime >> endTime;
      int startHour = stoi(startTime.substr(0,2));
      int startMinute = stoi(startTime.substr(3,2));
      int endHour = stoi(endTime.substr(0,2));
      int endMinute = stoi(endTime.substr(3,2));
      startSum += startHour*60+startMinute;
      endSum += endHour*60+endMinute;
    }
    cout << endSum - startSum;

    return 0;
}
```