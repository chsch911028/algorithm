# 다익스트라 알고리즘 구현

```java
/*
TEST CASE
8 11 0 6
0 1 3 
0 5 1
1 2 4
1 3 1
1 5 1
2 4 6
2 6 9
2 7 4
3 4 2
4 6 9
6 7 3

*/
import java.util.Scanner;
public class Main{
  
    public static final int MAX = 2010;
  
    public static void main(String[] args){

       // Please Enter Your Code Here
       Scanner sc = new Scanner(System.in);
       
       int n = sc.nextInt();
       int m = sc.nextInt();
       int start = sc.nextInt();
       int end = sc.nextInt();
       
       daijk(sc,n,m,start,end);
    }
    
    public static void daijk(Scanner sc, int n, int m, int start, int end){
      
      int v_len[] =  new int[MAX];
      int v[][] = new int[MAX][MAX];
      int w[][] = new int[MAX][MAX];
      
      //set graph
      for(int i=0; i<m; i++){
        int a = sc.nextInt();
        int b = sc.nextInt();
        int weight = sc.nextInt();
        
        //linking
        v[a][v_len[a]] = b;
        v[b][v_len[b]] = a;
        
        //weight
        w[a][v_len[a]++] = weight;
        w[b][v_len[b]++] = weight;
      }
      
      //T[i]: start부터 i 정점까지의 최단거리
      int T[] = new int[n];
      //checked[i]: T[i]의 최단거리가 확정됬는지 판단해줌
      boolean checked[] = new boolean[n];
      
      //최단거리이기 때문에, 가장큰값으로 초기화
      for(int i=0; i<n; i++){
        T[i] = 999999999;
      }
      
      //T[start] 최단거리 0으로 세팅->왜? 시작점이므로 
      T[start] = 0;
      
      //각 정점을 순회하며 최단거리를 설정
      for(int i=0; i<n; i++){
        
        int min = 999999999; int min_idx = -1;
        
        for(int j=0; j<n; j++){
          //아직 최단거리가 결정되지 않았고,
          //가장 작은 최소값을 갖는 정점을 추출해냄
          if(!checked[j] && T[j] < min){
            min = T[j];
            min_idx = j;
          }
        }//for j end
          
        //추출된 정점은 최단거리가 확정된 것임
        //왜? 모든 경로중에서 최단거리로 움직일 수 있는 정점이므로
        checked[min_idx] = true;
          
        //추출된(최단거리가 결정된) 정점에서 부터 뻗어나가면서
        for(int j=0; j < v_len[min_idx]; j++){
          int next_vertex = v[min_idx][j];
          int next_weight = w[min_idx][j];
          
          //인접한 정점의 최소값을 update
          if(next_weight + min < T[next_vertex]){
            T[next_vertex] = next_weight + min;
          }
        }//for j end
        
      }// for i end
      
      /* 정점 링크 + 가중치 확인용
      for(int i=0; i<n; i++){
        System.out.print(i+": ");
        String w_str = "";
        for(int j=0; j<v_len[i]; j++){
          System.out.print(v[i][j]+" ");
          w_str = w_str + w[i][j] + " ";
        }
        System.out.println("");
        System.out.println("   "+w_str);
      }
      */
      
      /* start 부터 모든(i번째) 정점까지의 최단거리 확인용
      for(int i=0; i<n; i++){
        System.out.print(T[i]+" ");  
      }
      */
      
      System.out.print(T[end]);
    }

}
```