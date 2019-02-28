# NN단표

### 문제

----------

알랩이는 구구단표처럼 NN단표를 만들었다고 한다.

NN단표는 2차원 배열의 모양으로 곱셈 1단부터 N단까지의 값들을 적어놓은 형태이다.

NN단표의 배열을 A라고 했을 때, 배열의 들어가는 수 A[i][j]=i*j이다.(즉, 4행 7열에는 28, 7행 5열에는 35가 들어가 있다.)

알랩이는 N단까지 나온 숫자들 중에서 K번째로 작은 수를 찾고 싶어한다.

이때, 중복되는 여러 수들을 고려한다. 즉 N*N개의 모든 수들 중에서 K번째 수를 구하는 것이다.

### 입력

----------

첫째 줄에 배열의 크기 N이 주어진다. N은 100,000보다 작거나 같은 자연수이다. 둘째 줄에 K가 주어진다. K는 N*N보다 작거나 같은 자연수이다.

### 출력

----------

K번째 원소를 출력한다.

### 예제 입력

```
3
7
```

### 예제 출력

```
6
```

### 코드

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){

      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      int n = Integer.parseInt(sc.nextLine());
      long k = Long.parseLong(sc.nextLine());
      
      long value = kValue(n,k,1,n*n);
      // long max = 0;
      // for(int i=1; i<=n; i++){
      //   for(int j=1; j<=n; j++){
      //     if(i*j <= value && i*j > max){
      //       max = i*j;
      //     }
      //   }
      // }
      System.out.println(value);
    }
    
    public static long kValue(int n, long k, long s, long e){
      
      if(e-s==1){
        return e;
      }
      
      long mid = (e+s)/2;
      long tot = 0;
      long max = 0;
      for(int i=1;i<=n;i++){
        long cnt = mid/i;
        if(cnt > n){ cnt = n; }
        if(cnt*i <= mid && cnt*i > max){ max = cnt*i;}
        tot = tot + cnt;
      }
      
      if(tot==k){ return max; }
      if(tot < k){ return kValue(n,k,mid,e); }
      if(tot > k){ return kValue(n,k,s,max); }
      
      return e;
    }
}
```