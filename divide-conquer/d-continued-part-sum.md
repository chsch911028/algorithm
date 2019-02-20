# 연속부분최대합

### 문제

----------

N개의 정수가 주어질 때, 연속된 부분을 선택하여 합을 최대화 하는 프로그램을 작성하시오. 예를 들어, 아래와 같이 8개의 숫자가 있을 경우, 색칠된 부분을 선택했을 때 그 합이 가장 최대가 된다.

![d-continued-part-sum](d-continued-part-sum.png)

### 입력

----------

첫 번째 줄에 n이 주어진다. ( 1 ≤ n ≤ 100,000 ) 두 번째 줄에 n개의 정수가 주어진다.

### 출력

----------

연속된 부분을 선택하였을 때의 최댓값을 출력한다.

### 예제 입력

```
8
2 3 -5 8 -3 4 2 -9
```

### 예제 출력

```
11
```

### 예제 입력

```
5
-1 -2 3 -2 4
```

### 예제 출력

```
5
```

### 코드

```java
import java.util.Scanner;
public class Main{
    
    public static final int MIN = -2147483648;
  
    public static void main(String[] args){

      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      int n = Integer.parseInt(sc.nextLine());
      String numStr[] = sc.nextLine().split(" ");
      int num[] = new int[n];
      
      //convert numStr into num
      for(int i=0; i<n; i++){
        num[i] = Integer.parseInt(numStr[i]);
      }
      //getMaxSum
      System.out.println(getMaxSum(num,0,n-1));
      
    }
    
    //1.getMaxSum(): 해당 범위의 연속된 값의 합의 최대값을 반환
    // int num[]: 숫자 배열
    // int s: 탐색 시작 인덱스
    // int e: 탐색 종료 인덱스
    // int min: 최소값 설정
    
    public static int getMaxSum(int num[], int s, int e){
      
      //Exit
      if(s == e){
        return num[s];
      }  
      
      //logic start #####
      int mid = (e+s)/2;
      int max = MIN;
      
      int left_max = MIN; int sum = 0;
      //left range of max sum( * move right to left )
      for(int i=mid; i>=s; i--){
        sum = sum + num[i];
        if(sum > left_max){ left_max = sum; }
      }
      
      int right_max = MIN; sum = 0;
      //right range of max sum( * move left to right )
      for(int i=mid+1; i<=e; i++){
        sum = sum + num[i];
        if(sum > right_max){ right_max = sum; }
      }
      
      if(left_max+right_max > max){ max = left_max+right_max; }
      //##### logic end
      
      //divide
      int left_part_max = getMaxSum(num, s, mid);
      int right_part_max = getMaxSum(num, mid+1, e);
      
      //conquer ( 더 작은 사례에서 얻어진 최대의 수와 현재 에서 구한 최대값 비교! )
      if(left_part_max > max){ max = left_part_max; }
      if(right_part_max > max){ max = right_part_max; }
      
      return max;
    }
}
```