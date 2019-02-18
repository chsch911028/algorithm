# 이상한 계산기

<br>

### 문제

----------

이상한 계산기는 두 가지 버튼과 숫자를 출력하는 화면으로 구성되어 있다. 숫자를 출력하는 화면은 총 5자리의 정수를 표현할 수 있다. 각 버튼은 현재까지의 계산 결과에 어떠한 연산을 할지를 나타내는 것으로, 각 버튼은 다음과 같이 연산을 수행한다.

-   Mul : 현재까지의 계산 결과에 2를 곱한다
-   Div : 현재까지의 계산 결과를 3으로 나눈다. 단, 결과가 정수가 아닐 경우, 소수점 이하를 모두 버린다. 계산기를 작동시키면, 현재까지의 계산 결과로써 1이 출력된다. 이후 사용자가 어떻게 버튼을 누르냐에 따라 출력되는 숫자가 달라진다. 예를 들어, 계산기를 작동시키면 1이 출력되고, 여기서 Mul를 누르면 2가 되며, 또 Mul을 누르면 4가 출력된다.

영수는 이 계산기가 모든 숫자를 출력할 수 있는지 궁금해졌다. 하지만 영수는 버튼을 누르는 것 조차 매우 귀찮은 일이기 때문에, 계산기의 버튼을 최대한 적은 횟수만큼만 누르고 싶어 한다. 숫자 N이 주어질 때, 계산기를 작동시켜 숫자 N을 만들기 위하여 최소 몇 번 버튼을 눌러야 하는지를 구하는 프로그램을 작성하시오. 예를 들어, 숫자 10을 만들기 위해서는 1 → 2 → 4 → 8 → 16 → 5 → 10 가 되게끔 버튼을 누르면 되므로, 버튼을 6번만 누르면 되고, 이것이 최솟값이다. 참고로, 이상한 계산기는 5자리 정수까지밖에 표현할 수 없으며, 만약 연산 결과가 5자리를 넘어가는 경우에는 계산기가 고장나버린다. 따라서 항상 계산 결과를 최대 5자리로 유지해야 한다.

### 입력

----------

첫째 줄에는 이상한 계산기로 만들고자 하는 숫자 N이 주어진다. ( 1 ≤ N ≤ 99,999 ) 단, 계산기로 만들 수 없는 값은 주어지지 않는다.

### 출력

----------

이상한 계산기로 숫자 N을 만들기 위해 눌러야 하는 최소 버튼 클릭 횟수를 출력한다.

### 예제 입력

```
10
```

### 예제 출력

```
6
```

### 코드

```java
import java.util.Scanner;
import java.util.Queue;
import java.util.LinkedList;

public class Main{
  
    public static final int MAX = 1000000;
    public static void main(String[] args){
       
       // Please Enter Your Code Here
       Scanner sc = new Scanner(System.in);
       int n = sc.nextInt();
       
       System.out.println(BFS(n));
    }
    
    //N이 되기 위해서 최소로 눌러야 하는 버튼의 갯수를 반환
    public static int BFS(int n){
      
      Queue<Integer> q = new LinkedList<Integer>();
      int checked[] = new int[MAX];
      
      //초기값 셋팅
      q.offer(1); // 초기값
      q.offer(0); // 눌린버튼 횟수
      checked[0] = 1;
      checked[1] = 1;
      
      //결과
      int res = 0;
      
      while(!q.isEmpty()){
        //**step을 queue에 같이 넣어준다.
        //그럼 v==n이 되었을때 몇번째 button을 클릭한것인지
        //바로 알 수 있다!
        
        int v = q.poll();
        int step = q.poll();
        
        // 출력된 수가 n과 같으면 프로그램 종료
        if(v == n){ res = step; break; }
        
        //Mul을 누르는 경우: 
        //q에 입력되지 않았고,(=> 왜? q에 이미 들어가 있는 수는 검사할 필요 없기 때문에)
        //5자리 이하의 수면 q에 넣는다.
        int mul_v = v*2;
        if(mul_v < 100000 && checked[mul_v] == 0){ 
          q.offer(mul_v);
          q.offer(step+1);
          checked[mul_v] = 1;
        }          

        //Div를 누르는 경우
        int div_v = v/3;
        if(checked[div_v] == 0){
          q.offer(div_v);
          q.offer(step+1);
          checked[div_v] = 1;
        }          

      } // Mul,Div로 만들수있는 수를 계속해서 탐색해나감
      
      return res;
    }
}
```