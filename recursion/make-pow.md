# 거듭제곱구하기L

### 문제

----------

n과 m이 주어질 때, n^m을 구하는 프로그램을 작성하시오. 단, n^m의 값이 커질 수 있기 때문에, 정답을 10,007 으로 나눈 나머지를 출력한다.

### 입력

----------

첫 번째 줄에 숫자 n과 m이 주어진다. ( 1 ≤ n ≤ 100, 1 ≤ m ≤ 1,000,000,000,000,000,000 )

### 출력

----------

첫째 줄에 nm을 10,007 으로 나눈 나머지를 출력한다.

### 예제 입력

```
3 4
```

### 예제 출력

```
81
```

### 코드

```java
import java.util.Scanner;
public class Main{
  
    public static final int divider = 10007;
  
    public static void main(String[] args){
    
      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      String inputs[] = sc.nextLine().split(" ");
      long n = Long.parseLong(inputs[0]);
      long m = Long.parseLong(inputs[1]);
      
      System.out.println(pow(n,m));
      
      //나눈 나머지 * 나눈 나머지 
      //이게 만약에 나누는 수보다 크거나 가틍면 나눈나머지로 return
      
    }
    
    public static long pow(long n, long m){
      
      //Exit
      if(m<=2){
        long res = 1;
        for(long i=1;i<=m;i++){
          res = res*n;
        }
        return (res%divider);
      }
      
      //divide
      long res = 1;
      
      //m이 홀수인 경우
      if(m%2 != 0){
        long dived_m = (m-1)/2;
        long return_val = pow(n,dived_m);
        res = return_val*return_val*n;
      }else{ //m이 짝수인 경우
        long dived_m = m/2;
        long return_val = pow(n,dived_m);
        res = return_val*return_val;       
      }
      
      return res%divider;
      
    }
}
```