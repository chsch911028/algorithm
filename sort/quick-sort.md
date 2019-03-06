# 퀵정렬 구현하기

### 문제

----------

N개의 자연수가 주어질 때, 퀵정렬을 이용하여 이를 정렬하는 프로그램을 작성하시오.

### 입력

----------

첫 번째 줄에 N이 주어진다. ( 1 ≤ N ≤ 100,000 ) 두 번째 줄에 N개의 자연수가 주어진다.

### 출력

----------

퀵정렬을 이용하여 숫자를 오름차순으로 정렬한 결과를 출력한다.

### 예제 입력

```
10
5 9 2 8 3 7 4 6 1 10
```

### 예제 출력

```
1 2 3 4 5 6 7 8 9 10
```

### 예제 입력

```
5
2 3 1 2 1
```

### 예제 출력

```
1 1 2 2 3
```


### 코드

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){

      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      int n = Integer.parseInt(sc.nextLine());
      String inputs[] = sc.nextLine().split(" ");
      int arr[] =  new int[n];
      for(int i=0; i<n; i++){
        arr[i] = Integer.parseInt(inputs[i]);
      }
      
      arr = quickSort(n,arr);
      
      for(int i=0; i<n; i++){
        System.out.print(arr[i]+" ");
      }
      System.out.println("");
    }
    
    public static int[] quickSort(int n, int arr[]){
      
      //탈출구
      if(n==1 || n==0){
        return arr; 
      }
      
      //1. 피봇설정
      int pivotIdx = 0;
      int pivot = arr[pivotIdx];
      
      
      //2. 왼쪽/오른쪽 분리
      int leftP = 0;
      int rightP = 0;
      int leftArr[] = new int[n];
      int rightArr[] = new int[n];
      
      //3.pivot 보다 작은 값들은 모두 왼쪽으로 이동됨
      for(int i=1; i<n; i++){
        if(arr[i] < pivot){ // lt
          leftArr[leftP++] = arr[i];
        }else{ //eq-gt
          rightArr[rightP++] = arr[i];
        }
      }
      
      
      //4. pivot인덱스를 기준으로 왼쪽/오른쪽 구분해서  다시 퀵 정렬
      //left
      leftArr = quickSort(leftP,leftArr);
      //right
      rightArr = quickSort(rightP,rightArr);
      
      //5. 정렬된 leftArr, rightArr을 원래 배열에 넣어줌
      for(int i=0; i<leftP; i++){
        arr[i] = leftArr[i];
      }
      arr[leftP] = pivot;
      for(int i=0; i<rightP; i++){
        arr[leftP+1+i] = rightArr[i];
      }
      
      return arr;
    }
}
```