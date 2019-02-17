# 깊이 우선 탐색과 너비 우선 탐색

<br>

### 문제

----------

그래프가 주어질 때, 0번 정점을 시작으로 하여 깊이우선탐색과 너비우선탐색의 결과를 출력하는 프로그램을 작성하시오. 단, 노드를 방문할 때는 노드 번호가 작은 순서대로 방문한다고 하자.

### 입력

----------

첫째 줄에 정점의 개수 N과 간선의 개수 M이 주어진다. (1 ≤ N ≤ 1,000, 1 ≤ M ≤ 100,000 ) 둘째 줄부터 간선의 정보가 주어진다. 각 줄은 두 개의 숫자 a, b로 이루어져 있으며, 이는 정점 a와 정점 b가 연결되어 있다는 의미이다.

### 출력

----------

첫 번째 줄에 깊이우선탐색 결과, 두 번째 줄에 너비우선탐색 결과를 출력한다.

### 예제 입력

```
9 12
0 1
0 2
0 3
1 5
2 5
3 4
4 5
5 6
5 7
5 8
6 7
7 8
```

### 예제 출력

```
0 1 5 2 4 3 6 7 8
0 1 2 3 5 4 6 7 8
```

### 코드

```java
import java.util.Scanner;
import java.util.ArrayList;
import java.util.Vector;
import java.util.LinkedList;
import java.util.Queue;
import java.util.Arrays;

public class Main{
  
    public static final int MAX = 1010;
  
    public static void main(String[] args){
      // PASS
      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      int v = sc.nextInt();
      int e = sc.nextInt();
      
      // 나의 인접리스트 만들어 그래프 표현하는 방식
      // Vecotr, ArrayList로 만들기 복잡함
      // 그냥 공간 많이 사용하자
      int v_len[] = new int[v];
      int list[][] = new int[v][MAX];//graph
      
      for(int i=0; i<e; i++){
        int a = sc.nextInt();
        int b = sc.nextInt();
        
        list[a][v_len[a]++] = b;
        list[b][v_len[b]++] = a;
      }
/*    
      //list(graph) 정점-간선 입력 내용 확인하기
      for(int i=0; i<v; i++){ //i는 정점
        System.out.print(i+": ");
        for(int j=0; j<v_len[i]; j++){// j는 간선
          System.out.print(list[i][j]+" ");
        }
        System.out.println(" ");
      }
*/    

      //Queue q = new LinkedList();
      //q.offer(x) : x 입력
      //q.poll() : 빼기
      //q.isEmpty() : 비었는지 확인
      //q.peek() : 나올 값이 무엇인지 확인만하기
      
      DFS(list, v_len, 0, new boolean[v]);
      System.out.println("");
      BFS(list, v_len);
      
    }
    
    public static void DFS(int list[][], int v_len[], int v, boolean visited[]){
      // 깊이 우선 탐색
      
      // 1. 내가 방문됬음을 표시한다.
      visited[v] = true;
      System.out.print(v+" ");
      
      // 2. 방문하지 않은 주변 정점들 중 작은 정점을 탐색한다.
      // 정렬하는 이유
      // (단, 작은 값을 갖는 노드를 우선적으로 방문한다.)
      Arrays.sort(list[v],0,v_len[v]);
      for(int i=0; i<v_len[v]; i++){
        int next = list[v][i];
        if(!visited[next]){
          // 3. 그 정점에서 DFS를 진행한다.(즉, 1,2를 반복한다)
          DFS(list, v_len, next, visited);
        }
      }
      
      // 4. 모든 주변 정점들이 방문됬다면 되돌아간다.
      
    }//DFS END
    
    public static void BFS(int list[][], int v_len[]){
      
      //너비 우선 탐색
      Queue<Integer> q = new LinkedList<Integer>(); //원형큐
      boolean checked[] = new boolean[v_len.length];
      
      //BFS는 큐에 초기값 설정후 진행!
      q.offer(0);
      checked[0] = true;      
      
      while(!q.isEmpty()){ // 4. 큐가 빈상태일때까지 반복한다.
        //1. 큐에서 방문할 정점을 뺀다
        int v = q.poll();
        System.out.print(v+" ");
        //2. 나와 연결된 정점을 탐색한다.
        // 정렬하는 이유(DFS에서 이미 했으므로 생략)
        // (단, 작은 값을 갖는 노드를 우선적으로 방문한다.)
        for(int i=0; i<v_len[v]; i++){
          int next = list[v][i];
          if(!checked[next]){
            //3. 큐에 입력되지 않은 정점을 모두 큐에 넣는다.
            q.offer(next);
            //4. 큐에 이미 입력되었음을 표시한다.
            checked[next] = true;
          }
        }
      }      
    } // BFS END
    
}
```