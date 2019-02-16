# 팰린드롬 만들기

<br>

### 문제

----------

팰린드롬이란, 앞으로 읽으나 뒤로 읽으나 똑같은 문자열을 말한다. 예를 들어, “abcba”, “abccba” 등이 있을 수 있다. 문자열이 주어질 때, 이를 팰린드롬으로 만들기 위하여 추가해야 하는 최소의 문자 개수를 출력하는 프로그램을 작성하시오. 예를 들어, 문자열이 “abca” 로 주어질 경우, ‘b’만 추가하면 “abcba” 를 만들 수 있으므로, 이 때는 1개의 문자만 추가하면 된다. 또 다른 예로써, 문자열이 “adcba” 로 주어질 경우에는, 문자 2개를 추가해야 한다.


### 입력

----------

첫 번째 줄에 문자열이 주어진다. 이 문자열의 길이는 1,000 을 넘지 않는다.

### 출력

----------

주어진 문자열을 팰린드롬으로 만들기 위해서 추가해야 하는 문자 개수의 최솟값을 출력한다.

### 예제 입력

```
adcba
```

### 예제 출력

```
2
```

### 예제 입력

```
abccbdbac
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
      //PASS
      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      //1. 입력받기
      String str = sc.nextLine();
      int n = str.length();
      
      //2. Table 구하기
      //   T[i][j]를 구하기 위해서는 아래 3가지가 필요함
      //   왼쪽: T[i][j-1]
      //   아래쪽: T[i+1][j]
      //   대각선: T[i+1][j-1];
      //   그래서 아래 왼쪽부터 값을 채워가는것이 필요함
      int T[][] = new int[n][n];
      int back_step = n-1;//col
      for(int row=n-2; row>=0; row--){
        for(int col=back_step; col<=n-1; col++){
          //T[i,j] = i부터 j번째 문자까지 팰린드롬이 되기 위해서 
          //         추가해야할 최소한의 문자 갯수
          //조건1) ch[i] == ch[j]: 같은 문자이면 
          //       i와 j의 사이에 있는 문자열이 팰린드롬이 되기위해
          //       가져야할 최소의 문자 갯수와 같다
          //       T[i][j] = T[i+1][j-1];
          char ch_i = str.charAt(row);
          char ch_j = str.charAt(col);
          if(ch_i == ch_j){ T[row][col] = T[row+1][col-1]; }
          else{
            //조건2) ch[i] != ch[j]: 다른 문자이면 두가지 경우를 비교 선택
            //       1) ch[j]를 ch[i] 앞쪽에 붙이는 경우
            //        => T[i][j-1] + 1
            //       2) ch[i]를 ch[j] 뒤쪽에 붙이는 경우
            //        => T[i+1][j] + 1          
            T[row][col] = minT(T, row, col-1, row+1, col) + 1;
          }
        }
        back_step--;
      }
      
      //4. 정답 => T[0][n-1] : 2차원배열 0번째 줄 끝 열
      System.out.println(T[0][n-1]);
    }
    
    public static int minT(int T[][], int i1, int j1, int i2, int j2){
      //T[i1][j1] T[i2][j2] 둘 중 작은값을 반환
      if(T[i1][j1] < T[i2][j2]){ return T[i1][j1]; }
      else{ return T[i2][j2]; } 
    }
    
}
```