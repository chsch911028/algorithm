
### 문제
숫자 1, 2, 3을 이용하여 숫자 N을 만드는 경우의 수를 출력하는 프로그램을 작성하시오. 예를 들어, N이 4일 경우에는 다음의 7가지 경우가 존재한다. 단, 경우의 수가 매우 많을 수 있으므로, 경우의 수를 1,000,007 로 나눈 나머지를 출력한다.

>1+1+1+1
1+1+2
1+2+1
2+1+1
2+2
1+3
3+1

### 입력
첫 번째 줄에 N이 주어진다. ( 1 ≤ N ≤ 100,000 )  

### 출력
1, 2, 3을 이용하여 N을 만들 수 있는 경우의 수를 1,000,007 로 나눈 나머지를 출력한다.  
<hr>

### 예제 입력
>4
### 예제 출력
>7
<hr>

### 예제 입력
>200
### 예제 출력
>290816
<hr>    

### 출처
Taejon 2001 PC번


```java
import java.util.Scanner;
public class Main{
    
    // PASS
    // T(i) : 1~M까지의 수로 i를 만드는 경우의 수
    // T(i) = T(i-1) + T(i-2) + T(i-3) + ... T(i-M)
    // 
    // 단, T(1) ~ T(M) 까지는 다른 방법으로 구해야함
    
    public static void main(String[] args){
      
      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      
      int n = sc.nextInt();
      int m = 3;
      int T[] = new int[n+1];
          T[1] = 1;
        //T[2] = T[1] + 1(자기자신);
        //T[3] = T[1] + T[2] + 1(자기자신);
      
      //1~M까지의 경우의 수 구하기
      int sum = T[1];
      for(int i=2; i<=m; i++){
        T[i] = sum + 1;
        sum = sum + T[i];
        if(T[i] >= 1000007){ T[i] = T[i]%1000007; }
      }
      
      //M+1~N까지의 경우의 수 구하기
      for(int i=m+1; i<=n; i++){
        for(int j=i-m; j<i; j++){
          T[i] = T[i] + T[j];
          if(T[i] >= 1000007){ T[i] = T[i]%1000007; }
        }
      }
	  
	  //각 경우의수 1000007으로 나눈 나머지를 합치면 됨
      
      //T[n] 출력
      System.out.println(T[n]);                    
    }        
}
```