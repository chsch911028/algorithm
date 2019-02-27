# 히스토그램에서 가장 큰 직사각형 찾기

### 문제

----------

히스토그램이란, 아래 그림과 같이 직사각형이 배열되어 있는 것을 말한다. 각 직사각형의 가로 길이는 1로 모두 같고, 세로 길이는 다를 수 있다. 예를 들어, 아래 그림은 높이가 2, 1, 4, 5, 1, 3, 3 인 직사각형으로 이루어진 히스토그램이다.

![히스토그램](histogram
.png)

히스토그램이 주어질 때, 가장 큰 직사각형의 너비를 출력하는 프로그램을 작성하시오. 위의 예제에서는 최대 직사각형의 너비가 그림과 같이 8이다.

### 입력

----------

첫째 줄에 히스토그램을 이루는 직사각형의 개수 N이 주어진다. ( 1 ≤ N ≤ 100,000 ) 둘째 줄에는 각 직사각형의 높이가 주어진다. 높이는 10,000보다 작은 양의 정수이다.

### 출력

----------

최대 직사각형의 너비를 출력한다.

### 예제 입력

```
7
2 1 4 5 1 3 3
```

### 예제 출력

```
8
```

### 출처

University of Ulm local contest 2003 H


### 코드

```java
//Stack을 이용해서 다시한번 풀기
import java.util.Scanner;
public class Main{
    public static void main(String[] args){

      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      int n = Integer.parseInt(sc.nextLine());
      int histo[] = new int[n];
      
      histo[0] = sc.nextInt();
      int maxSize = histo[0];
      
      for(int i=1; i<n; i++){
        histo[i] = sc.nextInt();
        if(histo[i] > maxSize){ maxSize = histo[i]; }
      }
      
      //
      for(int i=0; i<n; i++){
        int now_height = histo[i];
        
        //to right
        int count = 1;
        for(int j=i+1; j<n; j++){
          int next_height = histo[j];
          if(now_height > next_height){ break; }
          count++;
        }// for j end
        
        //to left
        for(int j=i-1; j>=0; j--){
          int before_height = histo[j];
          if(now_height > before_height){ break; }
          count++;
        }// for j end
        
        int sum = now_height*count;
        if(maxSize < sum){ maxSize = sum; }
        
      }//for i end
      
      
      System.out.println(maxSize);
      
    }
}
```