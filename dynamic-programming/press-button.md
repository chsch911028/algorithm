# 직사각형의 합   

<br>

### 문제

----------

철수에게는 빨간색, 초록색, 파란색 세 개의 버튼이 있다. 버튼 하나를 누를 때 마다 특정 점수를 얻을 수 있으며, 철수는 1초에 한 번씩 버튼을 누를 수 있다. 물론, 특정 시간에는 세 개의 버튼 중에서 한 개의 버튼만을 누를 수 있다. 각 시간마다 특정 버튼을 눌렀을 때 얻는 점수는 모두 다를 수 있다. 예를 들어, 시간 1에 빨간색, 초록색, 파란색 버튼에 대한 점수가 3, 5, 7 로 주어질 수 있다. 이 경우에는 파란색을 누르는 것이 점수를 가장 많이 얻을 수 있다. 물론, 시간 2에 각 버튼에 대한 점수는 또 다를 수 있다. 버튼을 누를 때에는 한 가지 규칙이 있는데, 연속하여 색깔이 같은 버튼을 두 번 누를 수 없다는 것이다. 예를 들어, 시간 1에 초록색 버튼을 눌렀다면, 시간 2에는 초록색 버튼을 누를 수 없다. 이와 같은 규칙으로 각 시간마다 버튼을 누른다고 할 때, 철수가 얻을 수 있는 점수의 최댓값을 출력하는 프로그램을 작성하시오.

### 입력

----------

첫 번째 줄에 철수에게 주어진 시간 N이 주어진다. ( 1 ≤ N ≤ 100,000 ) 두 번째 줄부터 N개의 시간에 대하여 빨간색, 초록색, 파란색 버튼을 눌렀을 때 얻을 수 있는 점수가 주어진다.

### 출력

----------

철수가 얻을 수 있는 점수의 최댓값을 출력한다.

### 예제 입력

```
3
27 8 28
18 36 40
7 20 8
```

### 예제 출력

```
87
```

### 코딩
 
```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){
      
      //PASS
      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      int n = sc.nextInt();
      int num[] = new int[n*3];
      int T[] = new int[n*3];
      
      //set RGB
      for(int i=0; i<n*3; i++){
        num[i]= sc.nextInt();
        //T[0],T[1],[2] 초기화
        if(i < 3){ T[i] = num[i];}
      }
      
      //T[i] =  num[i]를 갖으면서 가장 최대가 되는 값
      for(int i=3; i<n*3; i = i+3){
        for(int j=i; j<i+3; j++){
          //T[i-3](R), T[i-2](G), T[i-1](B) 중에서
          //자신과 다른 색상 2가지의 합 2가지를 비교해서
          //큰것을 선택한다
          if(j%3 == 0){ // 0(RED)
            int greenMax = T[i-2] + num[j];
            int blueMax = T[i-1] + num[j];
            T[j] = greenMax > blueMax ? greenMax : blueMax;
          }else if(j%3 == 1){ // 1(GREEN)
            int redMax = T[i-3] + num[j];
            int blueMax = T[i-1] + num[j];
            T[j] = redMax > blueMax ? redMax : blueMax;            
          }else{ // 2(BLUE)
            int redMax = T[i-3] + num[j];
            int greenMax = T[i-2] + num[j];
            T[j] = redMax > greenMax ? redMax : greenMax;                        
          }
        }//for j end
      }// for i end
      
      System.out.println(getMaxT(n*3,T));
    }
    
    //getMax: T[n-1], T[n-2], T[n-3] 중에서 가장 큰 값 반환
    public static int getMaxT(int n, int T[]){
      
      int max = T[n-3];
      if(T[n-2] > max){ max = T[n-2]; }
      if(T[n-1] > max){ max = T[n-1]; }
      
      return max;
    }
}
```