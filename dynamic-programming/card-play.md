
# 카드놀이

<br>

### 문제

----------

N개의 카드가 주어지고, 각각은 자연수의 점수를 가진다. 철수는 이제 이 카드를 가져감으로써 카드에 적혀있는 수 만큼의 점수를 얻는다. 단, 카드를 가져갈 때 한가지 규칙이 있는데, 이는 연속하여 3개의 카드는 가져갈 수 없다는 것이다. 예를 들어, 6개의 카드 “1 3 5 2 7 3”가 주어질 경우, 3+5+7+3 = 18 만큼의 점수를 얻는 것이 최대이다. N개의 카드가 주어질 때, 얻을 수 있는 점수의 최댓값을 출력하는 프로그램을 작성하시오.

### 입력

----------

첫 번째 줄에 N이 주어진다. ( 1 ≤ N ≤ 100,000 ) 두 번째 줄에 N개의 숫자가 주어지며, 이는 각 카드의 점수를 나타낸다.

### 출력

----------

얻을 수 있는 점수의 최댓값을 출력한다.

### 예제 입력

```
6
1 3 5 2 7 3
```

### 예제 출력

```
18
```

### 코딩

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){
      //PASS
      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      int n = sc.nextInt();
      int num[] = new int[n];
      for(int i=0; i<n; i++){
        num[i] = sc.nextInt();
      }
      
      //
      //T[i] = num의 i번째 숫자들의 합 중 가장큰 최대값
      int T[] = new int[n];
          T[0] = num[0];
          T[1] = T[0]+num[1];
      int count = 2;
      
      //T[2] 설정 -> 연속되는 3수를 판단해야 하므로 여기까지는 미리 설정
      
      T[2] = num[2];
      if(num[2]+num[1] > T[1]){
        T[2] = num[2]+num[1];
        count = 2;
      }else if(num[2]+num[0] > T[1]){
        T[2] = num[2]+num[0];
        count = 1;
      }else{
        T[2] = T[1];
        count = 0;
      }
      // System.out.println(T[2]+"/"+count);
      for(int i=3; i<n; i++){
        // System.out.println(i+"////////////////");
        //if count < 2 then T[i] = T[i-1] + num[i]; 
        if(count<2){
          T[i] = T[i-1] + num[i];
          count++; // 현재 num이 참여 했기때문에
        }else{
          //else(count >=2) 현재 2수가 연속되므로 2가지 경우 고려
          //1.num[i] 즉, 새로운수가 참여하는게 더 커지는 경우
          //T[i-1] < T[i-2] + num[i]
          if(T[i-1] < T[i-2] + num[i]){
            T[i] = T[i-2] + num[i];
            count = 1;
          }else{
            //2.num[i] 즉, 새로운수를 참여시키지 않는 경우
            //* 같은 경우: 현재수를 사용하지 않는것이 유리함
            //왜? 연속되는 카운트를 안해줘도 되기 때문에  
            T[i] = T[i-1];
            count = 0;
          }
          
          // T[i-3]+num[i]+num[i-1] 위에서 고려한 경우보다 큰경우
          if(T[i-3]+num[i]+num[i-1] > T[i]){
            T[i] = T[i-3]+num[i]+num[i-1];
            count = 2;
          }
        }
        // System.out.println(count+"/"+T[i]);
      } // for i end
      
      System.out.println(T[n-1]);
    }
}
```