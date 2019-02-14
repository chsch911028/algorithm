# 제곱수의 합

<br>

### 문제

----------

숫자 N을 제곱수의 합으로 표현하고자 할 때, 사용해야 하는 제곱 수의 최소 개수를 출력하는 프로그램을 작성하시오. 예를 들어, 숫자 45를 제곱수의 합으로 표현하고자 할 때 필요한 제곱 수의 최소 개수는 2개이며, 이는 다음과 같다.

```
45 = 3^2 + 6^2
```

### 입력

----------

첫 번째 줄에 N이 주어진다. ( 1 ≤ N ≤ 100,000 )

### 출력

----------

필요한 제곱 수의 최소 개수를 출력한다.

### 예제 입력

```
45
```

### 예제 출력

```
2
```

### 예제 입력

```
38
```

### 예제 출력

```
3
```

### 코드

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){
      //NO PASS.. 50
      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      int n = sc.nextInt();
      
      //T[i] = i를 제곱수를 표현하기 위해 가져야할 '최소 제곱의 수'
      int T[] = new int[n+1];
      
      for(int i=1; i<=n; i++){
        int j = 1;
        int pow = (int) Math.pow(j,2);
        if(pow == i){ T[i] = 1; continue; }
        T[i] = T[pow] + T[i-pow];
        
        while((int)Math.pow(j+1,2)<=i){
          j++;
          pow = (int)Math.pow(j,2);
          if(pow == i){ T[i] = 1; break; }
          if(T[i] > T[pow] + T[i-pow]){
            T[i] = T[pow] + T[i-pow];
          }
        }
      }
      
      // 2. T[n]는 T[pow]와 T[n-pow]의 합으로 이루어짐 
      System.out.println(T[n]);                  
    }
}
```