# 2색 칠하기

<br>

### 문제

----------

2색 칠하기란, 다음 두 조건을 만족하면서 그래프의 정점을 모두 색칠할 수 있는지 묻는 문제이다. 2개의 색이 존재한다. 인접한 두 정점은 색깔이 다르다. 그래프가 주어질 때, 2색 칠하기가 가능한지 출력하는 프로그램을 작성하시오. 예를 들어, 아래의 그래프는 2색 칠하기가 가능한 그래프이며, 정점을 색칠한 결과는 다음과 같다.

![fill-two-color](fill-two-color.PNG)

### 입력

----------

첫째 줄에 정점의 개수 N과 간선의 개수 M이 주어진다. ( 1 ≤ N ≤ 10,000, 1 ≤ M ≤ 100,000 ) 둘째 줄부터 간선의 정보가 주어진다. 각 줄은 두 개의 숫자 a, b로 이루어져 있으며, 이는 정점 a와 정점 b가 연결되어 있다는 의미이다.(0 ≤ a, b ≤ N-1)

### 출력

----------

주어진 그래프에 대하여 2색 칠하기를 할 수 있으면 YES, 할 수 없으면 NO를 출력한다.

### 예제 입력

```
9 10
0 1
0 2
0 3
1 5
2 5
3 4
5 6
5 8
6 7
7 8
```

### 예제 출력

```
YES
```

### 예제 입력

```
9 11
0 1
0 2
0 3
1 5
2 5
3 4
4 5
5 6
5 8
6 7
7 8
```

### 예제 출력

```
NO
```

### 코드 

```java
import java.util.Scanner;
import java.util.Queue;
import java.util.LinkedList;

public class Main{
    
    public static final int MAX = 1000;
  
    public static void main(String[] args){
      //PASS
      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      int v = sc.nextInt();
      int e = sc.nextInt();
      
      // make list(graph)
      int list[][] = new int[v][MAX];
      int v_len[] = new int[v];
      int start_v = 0;
      
      // link edge
      for(int i=0; i<e; i++){
        int a = sc.nextInt();
        int b = sc.nextInt();
        
        if(i==0){ start_v = a; }
        
        list[a][v_len[a]++] = b;
        list[b][v_len[b]++] = a;
      }
      
      System.out.println(BFS(list,v_len,start_v));
    }
    
    public static String BFS(int list[][], int v_len[], int start_v){
          
          String res = "YES";
          
          //너비 우선 탐색
          //원형큐
          Queue<Integer> q = new LinkedList<Integer>(); 
          boolean checked[] = new boolean[v_len.length];
          boolean color[] = new boolean[v_len.length];
          // color : false 1번 색상
          //       : true 2번 색상
          
          
          //BFS는 큐에 초기값 설정후 진행!
          q.offer(start_v);
          checked[start_v] = true;
          color[start_v] = true;
          
          while(!q.isEmpty()){ // 4. 큐가 빈상태일때까지 반복한다.
          
            boolean isAble = true;
            //1. 큐에서 방문할 정점을 뺀다
            int v = q.poll();
            boolean v_color = color[v];
            //2. 나와 연결된 정점을 탐색한다.
            for(int i=0; i<v_len[v]; i++){
              int next = list[v][i];
              if(!checked[next]){
                //3. 큐에 입력되지 않은 정점을 모두 큐에 넣는다.
                q.offer(next);
                //4. 큐에 이미 입력되었음을 표시한다.
                checked[next] = true;
                //5. 해당 정점에 색깔을 넣는다.
                color[next] = !v_color;
              }else{
                //이미 방문된경우 칠해야하는 색과
                //현재 칠해져있는 색이 같은지 비교한다.
                //같지 않으면 불가능한 경우이므로 종료한다. 
                if(color[next] != !v_color){
                  isAble = false;
                  res = "NO";
                  break;
                }
              }
            }//for END
            
            if(!isAble){ break; }
          }
          
          return res;
    } // BFS END
        
}
```