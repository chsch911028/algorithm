# Algorithm
알고리즘 공부하기(Learn Algorithm)



# 1. 분할정복(Divide and Conquer)
> **분할정복**이란?  
주어진 문제를 작은 사례로 나누고(Divide) 각각의 작은 문제들을 해결하여 정복(Conquer)하는 방법

### 분할정복 설계
1. 문제를 하나 이상의 작은 사례로 분할(Divide)한다
2. 작은 사례들을 각각 정복(Conquer)한다.
3. 작은 사례의 해답을 통합(Combine)하여 원래 문제를 해결한다

_[예] 이진탐색, 합병정렬, 퀵정렬, 최대값 찾기 등_

~~~
//합병정렬 알고리즘 구현

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
~~~