# 미로 찾기

<br>

### 문제

----------

아래와 같이 이동할 수 있는 길, 그리고 이동할 수 없는 벽으로 이루어진 크기 N x M 의 지도가 주어진다. 이 때, (N-1, 0) 에서 출발하여 (0, M-1) 까지 도착하는 최단거리를 출력하는 프로그램을 작성하시오. 아래 그림에 대하여 S에서 E까지 가는 최단거리는 22이다.

![out-maze](out-maze.png)

### 입력

----------

첫째 줄에 지도의 세로 길이 N과 지도의 가로 길이 M이 주어진다. ( 1 ≤ N, M ≤ 1,000 ) 둘째 줄부터 지도의 정보가 주어진다. 0은 이동할 수 있는 부분, 1은 이동할 수 없는 부분을 나타낸다.

### 출력

----------

(N-1, 0) 에서 출발하여 (0, M-1) 까지 이동하는 데 필요한 최단거리를 출력한다.

### 예제 입력

```
10 10
0 0 0 0 0 0 1 1 0 0
0 1 1 1 0 0 1 0 1 0
0 1 1 1 0 0 1 0 1 0
0 0 0 0 0 0 0 0 1 0
0 0 1 1 1 1 0 0 1 0
0 0 0 0 0 0 1 1 0 0
0 0 1 1 1 0 1 1 0 0
0 0 1 1 1 0 0 0 0 0
0 0 0 0 0 1 1 1 0 0
0 0 0 0 0 0 0 1 0 0
```

### 예제 출력

```
22
```

### 코드

```java
import java.util.Scanner;
import java.util.Queue;
import java.util.LinkedList;
//RUNTIME 이유:
//num이 계속해서 커지면서 백만이 들어가게되고
//그러면 array[num] 형태로 사용하게되면 RUNTIME ERROR가 나게됨

public class Main{
    
    public static void main(String[] args){

      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      int n = sc.nextInt();
      int m = sc.nextInt();
      
      //set map
      int map[][] = new int[n][m];
      for(int i=0; i<n; i++){
        for(int j=0; j<m; j++){
          map[i][j] = sc.nextInt();
        } // for j end
      }//for i end
      
      BFS(map, n, m);
    }

    public static void BFS(int map[][], int n, int m){
      
      //너비 우선 탐색
      Queue<Integer> q = new LinkedList<Integer>(); //원형큐
      int step[][] = new int[n][m];
      
      //BFS는 큐에 초기값 설정후 진행!
      //S(n-1, 0)
      q.offer(n-1);
      q.offer(0);
      
      while(!q.isEmpty()){ 
        //1. 큐에서 방문할 정점을 뺀다
        int i = q.poll();
        int j = q.poll();
        int now_step = step[i][j];
        
        //위쪽
        int up_i = i-1;
        int up_j = j;
        
        //오른쪽
        int right_i = i;
        int right_j = j+1;
        
        //아래쪽
        int down_i = i+1;
        int down_j = j;

        //왼쪽
        int left_i = i;
        int left_j = j-1;
        
        //2. 이동가능한 블럭인지 확인
        //   이미체크된 블럭인지 확인
        //   스텝저장(=방문체크) + 큐에 입력
        //위쪽
        if(up_i >= 0 && map[up_i][up_j] == 0 && step[up_i][up_j] == 0){
          step[up_i][up_j] = now_step+1;
          q.offer(up_i);
          q.offer(up_j);
        }
        
        //오른쪽
        if(right_j < m && map[right_i][right_j] == 0 && step[right_i][right_j] == 0){
          step[right_i][right_j] = now_step+1;
          q.offer(right_i);
          q.offer(right_j);
        }
        
        //아래쪽
        if(down_i < n && map[down_i][down_j] == 0 && step[down_i][down_j] == 0){
          step[down_i][down_j] = now_step+1;
          q.offer(down_i);
          q.offer(down_j);
        }
        
        //왼쪽
        if(left_j >= 0 && map[left_i][left_j] == 0 && step[left_i][left_j] == 0){
          step[left_i][left_j] = now_step+1;
          q.offer(left_i);
          q.offer(left_j);
        }        
        
      }// 3. 큐가 빈상태일때까지 반복한다.
      
      //E(0, m-1)
      /*
      for(int i=0; i<n; i++){
        for(int j=0; j<m; j++){
          System.out.print(step[i][j]+" ");
        }
        System.out.println(" ");
      }
      */
      System.out.println(step[0][m-1]);
    } // BFS END   
    
}

```