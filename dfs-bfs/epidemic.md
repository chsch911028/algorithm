# 전염병

<br>

### 문제

----------

철수네 마을에는 갑자기 전염병이 유행하기 시작하였다. 이 전염병은 전염이 매우 강해서, 이웃한 마을끼리는 전염되는 것을 피할 수 없다.  
철수네 마을은 1번부터 N번까지 번호가 매겨져 있다. 철수네 마을의 구조는 꽤나 복잡한데, i번 마을에서 출발하면 i * 2 번 마을에 갈 수 있고, 또한 i / 3(i를 3으로 나눈 몫) 번째 마을에도 갈 수 있다. 전염병은 사람에 의하여 옮는 것으로 알려져 있다. 따라서 i번 마을에 전염병이 돌게 되면, i * 2 번 마을과 i / 3(i를 3으로 나눈 몫) 번 마을 역시 전염병이 돌게 된다.  
K번 마을이 가장 처음으로 전염병이 돌기 시작했을 때, 전염병이 돌지 않는 마을의 개수를 구하는 프로그램을 작성하시오.

### 입력

----------

첫째 줄에 전체 마을의 개수 N과, 처음으로 전염병이 돌기 시작한 마을 번호 K가 주어진다. ( 1 ≤ N, K ≤ 100,000 )

### 출력

----------

전염병이 돌지 않는 마을의 개수를 출력한다.

### 예제 입력

```
10 3
```

### 예제 출력

```
4
```

### 코드

```java
import java.util.Scanner;
import java.util.Queue;
import java.util.LinkedList;

public class Main{
    public static void main(String[] args){

      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      int n = sc.nextInt();
      int k = sc.nextInt();
      
      System.out.println(BFS(n,k));
    }
    
    //BFS: 1~n까지의 마을중에서 전염되지 않은 마을의 갯수 반환
    //     전염은 K번째 마을에서 부터 시작됨.
    public static int BFS(int n, int k){
      
      Queue<Integer> q = new LinkedList<Integer>();
      boolean checked[] = new boolean[n+1];
      
      //1.초기값 셋팅
      q.offer(k);
      checked[k] = true;
      
      int cnt = 0;
      
      while(!q.isEmpty()){
        //1. 전염된 마을 추출 + 카운팅
        int v = q.poll();
        cnt++;
        
        //2. 전염된 마을의 *2 번째 마을 방문
        //   아직 검사되지 않은 마을인 경우
        //   마을의 번호는 n을 넘어갈 수 없으므로 n이하의 마을번호를 갖는다면
        int mul_v = v*2;
        if(mul_v <= n && !checked[mul_v]){
          q.offer(mul_v);
          checked[mul_v] = true;
        }
        //3. 전염된 마을의 /3 번째 마을 방문
        //   아직 검사되지 않았은 마을인 경우
        //   마을의 번호는 1부터 시작하므로 0보다 큰 마을인경우
        int div_v = v/3;
        if(div_v > 0 && !checked[div_v] ){
          q.offer(div_v);
          checked[div_v] = true;
        }
      }//4. 가능한 모든 마을을 방문할때까지 게속!
      
      return n-cnt; // 감연되지 않은 마을 갯수 반환
    }
}
```