# 합병정렬 구현하기(분할정복으로 다시 풀어보기!)

### 문제

----------

서로 다른 n개의 정수가 주어질 때, 이를 합병정렬을 이용하여 오름차순으로 정렬하는 프로그램을 작성하시오.

### 입력

----------

첫 번째 줄에 n이 주어진다. ( 1 ≤ n ≤ 100,000 ) 두번째 줄에 n개의 정수가 주어진다.

### 출력

----------

첫 번째 줄에 n개의 숫자를 합병정렬을 이용하여 오름차순으로 정렬한 결과를 출력한다.

### 예제 입력

```
10
2 5 3 4 8 7 -1 9 10 2
```

### 예제 출력

```
-1 2 2 3 4 5 7 8 9 10
```

### 코드

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){
      /* 내가 구현해보기 */
      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      int n = Integer.parseInt(sc.nextLine());
      String inputs[] = sc.nextLine().split(" ");
      
      int num[] = new int[n];
      for(int i=0; i<inputs.length; i++){
        num[i] = Integer.parseInt(inputs[i]);
      }
      int arr[] = mergeSort(n, num);
      for(int i=0; i<arr.length; i++){
        System.out.print(arr[i]+" "); 
      }
      System.out.println("");
    }
    
    /*
      //1. 매개변수
        - n
        - arr[]
      //2. 탈출구
        - n==1
      //3. 로직
       
    */    
    
    public static int[] mergeSort(int n, int arr[]){
      
      //탈출
      if(n == 1){
        return arr;
      }
      
      //로직
      int left = n/2;
      int right = n-left;
      
      //sliced LeftArr      
      int sLeftArr[] = new int[left];
      for(int i=0;i<left;i++){
        sLeftArr[i] = arr[i];
      }
      
      //sliced RightArr
      int sRightArr[] = new int[right];
      for(int i=0;i<right;i++){
        sRightArr[i] = arr[left+i];
      }
      
      int newArr[] = new int[n];
      int leftArr[] = mergeSort(left, sLeftArr);
      int rightArr[] = mergeSort(right, sRightArr);
      
      int leftIdx = 0;
      int rightIdx = 0;
      
      int ltNum = left < right ? left : right;
      int i=0;
      for( ; leftIdx < left && rightIdx < right; i++){
        if(leftArr[leftIdx] < rightArr[rightIdx]){
          newArr[i] = leftArr[leftIdx++]; 
        }else{
          newArr[i] = rightArr[rightIdx++]; 
        } 
      }
      
      while(leftIdx < left){
        newArr[i++] = leftArr[leftIdx++];
      }
      
      while(rightIdx < right){
        newArr[i++] = rightArr[rightIdx++];
      }
      
      return newArr;
    }
}
```