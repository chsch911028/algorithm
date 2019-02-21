# goodseq

### 문제

----------

숫자 1, 2, 3으로만 이루어지는 수열이 있다. 임의의 길이의 인접한 두 개의 부분 수열이 동일한 것 이 있으면, 그 수열을 나쁜 수열이라고 부른다. 그렇지 않은 수열은 좋은 수열이다.

다음은 나쁜 수열의 예이다.

3**3**

3**2121**323

**123123**213

다음은 좋은 수열의 예이다.

2

32

32123

1232123

길이가 N인 좋은 수열들을 N자리의 정수로 보아 그중 가장 작은 수를 나타내는 수열을 구하는 프로그램 을 작성하라. 예를 들면, 1213121과 2123212는 모두 좋은 수열이지만 그 중에서 작은 수를 나타내는 수 열 1213121이다.

### 입력

----------

입력은 숫자 N하나로 이루어진다. N은 1 이상 80 이하이다.

### 출력

----------

첫 번째 줄에 1, 2, 3으로만 이루어져 있는 길이가 N인 좋은 수열들 중에서 가장 작은 수를 나타내 는 수열만 출력한다. 수열을 이루는 1, 2, 3들 사이에는 빈칸을 두지 않는다.

### 예제 입력

```
7
```

### 예제 출력

```
1213121
```

### 출처

----------

KOI 1997 중등부 1번

### 코드

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){

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

```