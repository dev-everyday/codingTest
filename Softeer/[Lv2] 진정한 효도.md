
# 문제

https://softeer.ai/practice/7374


# 풀이

정말 2단계 기준을 모르겠다.
field를 우선 scanf로 받은 이후에 각 i, j 와 j, i로 컬럼별, 로우별 합을 구한다.
이 때 abs를 통해서 k를 1부터 3으로 해서 차를 더했을 때 최솟값을 구해서 출력해주면 된다.

# 코드
```
#include<iostream>
#include<algorithm>
using namespace std;
int field[4][4];

int main(int argc, char** argv)
{
    int min_sum = 100;
    for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            scanf("%d", &field[i][j]);
        }
    }
    for(int i=0;i<3;i++){
        for(int k=1;k<4;k++){
            int col_sum = 0;
            int row_sum = 0;
            for(int j=0;j<3;j++){
                col_sum+=abs(k-field[j][i]);
                row_sum+=abs(k-field[i][j]);
            }
            min_sum = min(min_sum, col_sum);
            min_sum = min(min_sum, row_sum);
        }
    }
    printf("%d\n", min_sum);
    return 0;
}
```
```
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int[][] field = new int[3][3];
        int minSum = Integer.MAX_VALUE;

        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                field[i][j] = sc.nextInt();
            }
        }

        for (int k = 1; k <= 3; k++) { 
            for (int i = 0; i < 3; i++) {
                int colSum = 0;
                int rowSum = 0;

                for (int j = 0; j < 3; j++) {
                    colSum += Math.abs(k - field[j][i]);
                    rowSum += Math.abs(k - field[i][j]);
                }

                minSum = Math.min(minSum, colSum);
                minSum = Math.min(minSum, rowSum);
            }
        }

        System.out.println(minSum);
        sc.close();
    }
}

```