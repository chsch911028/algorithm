# 전염병

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
import java.util.LinkedList;
import java.util.Queue;

public class Main{
    public static void main(String[] args){

      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      String inputs[] = sc.nextLine().split(" ");
      int n = Integer.parseInt(inputs[0]);
      int k = Integer.parseInt(inputs[1]);
      
      Queue<Integer> q = new LinkedList<Integer>();
      int answer[] = new int[n+1];
      int cnt = 0;
      
      int base = k*2;
      for(int i=k; i<=n; i++){
        if(i == k){
          q.offer(i);
          answer[i] = 1;
        }
        if(i == base){
          q.offer(i);
          base = i*2;
          answer[i] = 1;
        }
      }
      
      
      while(!q.isEmpty()){
        int val = q.poll();
        cnt++;
        
        while(val >= 3){ // 나눠지는수 다시 큐에 삽입
          int check = 0;
          val = val/3;
          if(answer[val] == 0){ 
            q.offer(val);
            answer[val] = 1;
          }
          
          int base2 = val*2;
          while(base2 <= n && answer[base2] != 1){
            q.offer(base2);
            answer[base2] = 1;
            base2 = base2*2;
          } // while end          
          
        } // while end
        
      } // while end      
      
      // for(int i=0; i<n+1; i++){
      //   if(answer[i] == 1){
      //     System.out.println(i);  
      //   }
      // }
      
      System.out.println(n-cnt);
    }
}
```