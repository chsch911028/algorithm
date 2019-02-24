# 큐 구현하기

### 문제

----------

이 문제에서는 큐를 구현한다. 큐는 다음 세 개의 연산을 지원한다.

-   Push X : 큐에 정수 X를 push한다. 만약 rear 포인터가 더 이상 뒤로 갈 수 없다면, “Overflow”를 출력한다.
-   Pop : 큐에서 정수 하나를 pop한다. 만약 front 포인터가 더 이상 뒤로 갈 수 없다면, “Underflow”를 출력한다.
-   Front : 큐의 front에 있는 정수를 출력한다. 만약 큐가 비어있다면 “NULL”을 출력한다.

크기가 n인 큐에 m개의 연산을 하는 프로그램을 작성하시오. 입력의 편의를 위해서 Push는 “1”, Pop은 “2”, Top은 “3”으로 표현한다.

### 입력

----------

첫째 줄에 큐의 크기 n, 연산의 개수 m이 주어진다. ( 1 ≤ n ≤ 100, 1 ≤ m ≤ 1,000 ) 두 번째 줄부터 연산이 주어진다. 1은 Push, 2는 Pop, 3은 Front 연산을 의미한다.

### 출력

----------

연산의 결과를 출력한다.

### 예제 입력

```
4 15
1 1
1 2
1 3
3
2
2
3
1 4
1 5
3
2
2
1 6
2
3
```

### 예제 출력

```
1
3
Overflow
3
Overflow
Underflow
NULL
```

### 코드

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){

       // Please Enter Your Code Here
       Scanner sc = new Scanner(System.in);
       String inputs[] = sc.nextLine().split(" ");
       int size = Integer.parseInt(inputs[0]);
       int m = Integer.parseInt(inputs[1]);
       
       Queue q = new Queue(size);
       
       for(int i=0; i<m; i++){
         String op_val[] = sc.nextLine().split(" ");
         int op = Integer.parseInt(op_val[0]);
         // 1: push, 2: pop, 3:front
         int res = 0;
         switch(op){
           case 1: 
             int val = Integer.parseInt(op_val[1]);
             res = q.push(val);
             if(res != 0){
               System.out.println("Overflow");
             }
             break;
           case 2:
             res = q.pop();
             if(res == -1){
               System.out.println("Underflow");
             }
             break;
           case 3:
             res = q.front();
             if(res == -1){
               System.out.println("NULL");
             }else{
               System.out.println(res);
             }
             break;
           default:
             break;
         }
       }

    }
}


class Queue{
  int size;
  int data[];
  int f;
  int r;
  
  public Queue(int size){
    this.size = size;
    this.data = new int[size];
    this.f = 0;
    this.r = 0;
  }
  
  int push(int x){
    if(this.r >= size || this.r-this.f >= this.size){ return 1;  }
    else{ this.data[this.r++] = x; return 0; }
  }
  
  int pop(){
    if(this.r-this.f <= 0){ return -1; }
    else{ this.data[this.f] = 0; this.f++; return 0; }
  }
  
  int front(){
    if(this.r-this.f <= 0){ return -1; }
    else{ return this.data[this.f]; } 
  }
  
  int size(){
    return r-f;
  }
}
```