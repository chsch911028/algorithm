# 연속부분최대의 합

<br>

### 문제

----------

N개의 정수가 주어질 때, 연속된 부분을 선택하여 합을 최대화 하는 프로그램을 작성하시오. 예를 들어, 아래와 같이 8개의 숫자가 있을 경우, 색칠된 부분을 선택했을 때 그 합이 가장 최대가 된다.

![연속부분최대합](continued-part-sum.png)

### 입력

----------

첫 번째 줄에 n이 주어진다. ( 1 ≤ n ≤ 1,000,000 ) 두 번째 줄에 n개의 정수가 주어진다.

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
  
    public static final int MIN = -2000000000;
    
    public static void main(String[] args){
      //PASS
      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      int n = sc.nextInt();
      
      //점화식
      //T(i) = i번째 수를 끝으로 하는 연속 부분의 합중에서
      //       가장 큰 수
      //T(i) = max(T(i-1)+num(i), num(i))
      
      int T[] = new int[n];
          T[0] = sc.nextInt();
      int maxT = MIN;
      for(int i=1; i<n; i++){
        int num = sc.nextInt();
        T[i] = max(T[i-1]+num, num);
        if(T[i] > maxT){ maxT = T[i]; }
      }
      
      //풀이
      System.out.println(maxT);
      
    }
    
    public static int max(int a, int b){
      if(a > b){
        return a;
      }else{
        return b;
      }
    }
}
```