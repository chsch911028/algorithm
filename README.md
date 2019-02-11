# Algorithm
알고리즘 공부하기(Learn Algorithm)

# *알고리즘 CHECK LIST*

### 1. 배열의 범위를 조금더 선언할 것
### 2. 시뮬레이션 중 발생할 수 있는 초기화에 주의할 것
### 3. 2차월 배열(상,하,좌,우,대각선)을 탐색하는 경우 주변 배열을 1칸씩 더 선언하고 -1로 초기화한다
### 4. 문제를 정확히 이해하는 것이 중요하다
### 5. 최초에 발견한 솔루션을 한번 더 생각해보자(설계에 시간을 많이 쓰자)
### 6. 잘 보이지 않는 반례에 집중하자
### 7. 1억 미만의 반복이라면 컴퓨터에게 맡기자(복잡한것보다 1억미만 반복이 좋다)
### 8. 오늘 풀 수 있다고, 내일 풀 수 있는 것 아니다. 1,2주 이내에 복습하자



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


# 2. 재귀함수(Recursion)
> **재귀함수**란?
자신의 함수 내에서 다시 자기 자신을 호출하는 함수

### 재귀함수 설계
1. 어떤함수인지 명확하게 정의한다
2. 탈출구(기저조건)을 설정한다
3. 해결한 문제에 대한 로직을 구현한다

_[예] 팩토리얼 문제_
~~~
//좋은 순열로 이루어진 수 중 가장 작은 값을 판단하는 문제

import java.util.Scanner;
public class Main{
    public static void main(String[] args){
      //PASS
      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      int n = Integer.parseInt(sc.nextLine());
      String seq = "";
      String min[] = new String[1];
      
      getGoodSeq(n, seq, 0, min);
      
      System.out.println(min[0]);
    }
    
    //1. getGoodSeq() : 좋은 순열중 가장 작은 값을 판단하는 함수
    //2.   seq : 1,2,3중 한수를 채워 순열을 이루는 문자열 수
    //       n : 총순열 길이
    //     idx : arr의 index
    //    min[]: 현재 최소값을 갖는 수
    public static void getGoodSeq(int n, String seq, int idx, String min[]){
      
      //Exit
      if(idx == n){
        min[0] = seq;
        return; 
      } 
      
      //set 1
      if(min[0] == null && isValidSeq(seq+"1",0,idx)){
        getGoodSeq(n, seq+"1", idx+1, min);  
      }
      //set 2
      if(min[0] == null && isValidSeq(seq+"2",0,idx)){
        getGoodSeq(n, seq+"2", idx+1, min);
      }
      //set 3
      if(min[0] == null && isValidSeq(seq+"3",0,idx)){
        getGoodSeq(n, seq+"3", idx+1, min);
      }
      
      return;
    }
    
    //1. isValidSeq() : 좋은 순열인지 판단하는 함수
    //2.            s : 검사할 순열의 시작 index
    //              e : 검사할 순열의 마지막 index
    //            seq : 검사할 문자열 순열
    public static boolean isValidSeq(String seq, int s, int e){
      //Exit1
      //오른쪽 두개 셋트만 비교
      //(나머지는 어차피 이전에 비교되 통과된 수이기 때문에)
      int unit = (e-s+1)/2;
      boolean unit_res = true;
      while(unit > 0){
        String last_str = seq.substring(e-unit+1);
        String last_left_str = seq.substring(e-(unit*2)+1, e-unit+1);  
        if(last_str.equals(last_left_str)){ unit_res=false; break; }
        unit--;
      }
      
      return unit_res;
    }
    
    //1. isALTB(): A가 B보다 작은 수이면 True 반환
    //2. String a: 비교할 문자열 숫자 A
    //   String b: 비교할 문자열 숫자 B
    //              A와 B는 같은 길이의 문자열이다
    //      int s: 문자열 비교를 시작할 index  
    //      int e: 문자열 비교를 끝낼 index
    // 9223372036854775808 19자리
    
    public static int isALTB(String a, String b, int s, int e){
      // return -1 : a<b;
      // return  0 : same;
      // return  1 : b<a;
      
      //Exit
      if(e-s < 19){ // long으로 변환해서 판단 가능
        long a_long = Long.parseLong(a.substring(s,e));
        long b_long = Long.parseLong(b.substring(s,e));
        
        if(a_long == b_long){ return 0; }
        else if(a_long < b_long){ return -1; }
        else{ return 1; } // b<a
      }
      
      int mid = (e+s)/2;
      
      int result = -1;
      switch(isALTB(a,b,s,mid)){
        case -1: result=-1; break;
        case  0: result=isALTB(a,b,mid,e); break;
        case  1: result=1; break;
        default: break;
      }
      
      return result;
    }
  
  
}   

~~~

# 3. 동적 프로그래밍(Dynamic Programming)
> **동적 프로그래밍**이란?
부분 문제를 해결하여 전체 문제를 해결하는 알고리즘 방법

### _동적 프로그래밍 vs 분할 정복법_
* 동적 프로그래밍(Bottom Up) : "나" 보다 작은 문제의 풀이를 먼저 해결하고 *기억!* 즉, 밑에서 부터 해결해 올라오는 방식
* 분할 정복법(Top Down) : 큰 문제를 쪼개 내려가는 방식

### 동적 프로그래밍 설계
1. 부분 문제를 명확하게 정의한다
2. 점화식을 구한다
3. 점화식을 기반으로 문제를 해결한다

_[예] 피보나치 수 구하기_

~~~
ulong fibonacci_with_dynamic(int n) {
  int i = 0;
  ulong result = 0;
  ulong* fibonacci_tbl = 0;

  if (n == 0 || n == 1) {
    return n;
  }

  fibonacci_tbl = (ulong*) malloc((n+1) * sizeof(ulong));
  fibonacci_tbl[0] = 0;
  fibonacci_tbl[1] = 1;

  for (i = 2; i <= n; i++) {
    fibonacci_tbl[i] = fibonacci_tbl[i - 1] + fibonacci_tbl[i - 2];
  }

  result = fibonacci_tbl[n];

  free(fibonacci_tbl);

  return result;
}
~~~

_[예] 카드놀이_

~~~
/*
문제 : N 개의 카드가 주어질때, 숫자의 합이 최대가 되도록 카드를 뽑고, 그 최대 수를 출력하세요. (단, 3개의 연속된 순서로 있는 카드를 뽑을 수는 없음)
*/

import java.util.Scanner;
public class Main{
    public static void main(String[] args){
      //PASS
      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      int n = sc.nextInt();
      int num[] = new int[n];
      for(int i=0; i<n; i++){
        num[i] = sc.nextInt();
      }
      
      //
      //T[i] = num의 i번째 숫자들의 합 중 가장큰 최대값
      int T[] = new int[n];
          T[0] = num[0];
          T[1] = T[0]+num[1];
      int count = 2;
      
      //T[2] 설정 -> 연속되는 3수를 판단해야 하므로 여기까지는 미리 설정
      
      T[2] = num[2];
      if(num[2]+num[1] > T[1]){
        T[2] = num[2]+num[1];
        count = 2;
      }else if(num[2]+num[0] > T[1]){
        T[2] = num[2]+num[0];
        count = 1;
      }else{
        T[2] = T[1];
        count = 0;
      }
      // System.out.println(T[2]+"/"+count);
      for(int i=3; i<n; i++){
        // System.out.println(i+"////////////////");
        //if count < 2 then T[i] = T[i-1] + num[i]; 
        if(count<2){
          T[i] = T[i-1] + num[i];
          count++; // 현재 num이 참여 했기때문에
        }else{
          //else(count >=2) 현재 2수가 연속되므로 2가지 경우 고려
          //1.num[i] 즉, 새로운수가 참여하는게 더 커지는 경우
          //T[i-1] < T[i-2] + num[i]
          if(T[i-1] < T[i-2] + num[i]){
            T[i] = T[i-2] + num[i];
            count = 1;
          }else{
            //2.num[i] 즉, 새로운수를 참여시키지 않는 경우
            //* 같은 경우: 현재수를 사용하지 않는것이 유리함
            //왜? 연속되는 카운트를 안해줘도 되기 때문에  
            T[i] = T[i-1];
            count = 0;
          }
          
          // T[i-3]+num[i]+num[i-1] 위에서 고려한 경우보다 큰경우
          if(T[i-3]+num[i]+num[i-1] > T[i]){
            T[i] = T[i-3]+num[i]+num[i-1];
            count = 2;
          }
        }
        // System.out.println(count+"/"+T[i]);
      } // for i end
      
      System.out.println(T[n-1]);
    }
}

~~~

# 4. 시뮬레이션/완전탐색 (Brute Force)

