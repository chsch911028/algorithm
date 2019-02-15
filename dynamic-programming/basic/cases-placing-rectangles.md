# 직사각형 배치의 경우의 수 

<br>

### 문제

----------

2 x N 직사각형 모양의 칸이 있다. 이를 2 x 1 모양의 타일로 가득 채우려 한다. 가능한 경우의 수를 출력하는 프로그램을 작성하시오. 단, 가능한 경우의 수가 매우 많을 수 있으므로, 그 경우의 수를 1,000,007 로 나눈 나머지를 출력한다.

예를 들어, N = 3 일 경우에는 다음 세 가지의 가능한 경우가 존재한다.

<p align="center">
  <img src="cases-placing-rectangles.png">
</p>

### 입력

----------

첫 번째 줄에 N이 주어진다. ( 1 ≤ N ≤ 100 )

### 출력

----------

가능한 경우의 수를 1,000,007 로 나눈 나머지를 출력한다.

### 예제 입력

```
3
```

### 예제 출력

```
3
```

### 예제 입력

```
8
```

### 예제 출력

```
34
```

### 예제 입력

```
37
```

### 예제 출력

```
87896
```

### 코드

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){
      
      //PASS
      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      int n = sc.nextInt();
      int T[] = new int[n];
          T[0] = 1;
          T[1] = 2;
      
      //문제를 분석해보면 피보나치 수열과 같다는 것을 알 수 있음
      //1 2 3 5 8
      for(int i=2; i<n; i++){
        T[i] = T[i-1] + T[i-2];
        if(T[i] >= 1000007){ T[i] = T[i]%1000007; }
      }
      
      System.out.println(T[n-1]);
      
    }
}
```