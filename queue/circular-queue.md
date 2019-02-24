# 원형큐 구현하기


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
  int cnt;
  
  public Queue(int size){
    this.size = size;
    this.data = new int[size];
    this.f = 0;
    this.r = 0;
    this.cnt = 0;
  }
  
  int push(int x){
    if(this.cnt >= this.size){ return 1;  }
    else{ 
      this.data[this.r++] = x;
      this.cnt++;
      if(this.r >= size){ this.r = 0; }
      return 0;
    }
    
  }
  
  int pop(){
    if(this.cnt <= 0){ return -1; }
    else{ 
      this.data[this.f++] = 0;
      this.cnt--;
      if(this.f >= size){ this.f = 0; }
      return 0;
    }
  }
  
  int front(){
    if(this.cnt <= 0){ return -1; }
    else{ return this.data[this.f]; } 
  }
  
  int size(){
    return this.cnt;
  }
}
```

### 코드

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){
       //PASS
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
  int cnt;
  
  public Queue(int size){
    this.size = size;
    this.data = new int[size];
    this.f = 0;
    this.r = 0;
    this.cnt = 0;
  }
  
  int push(int x){
    if(this.cnt >= this.size){ return 1;  }
    else{ 
      this.data[this.r++] = x;
      this.cnt++;
      if(this.r >= size){ this.r = 0; }
      return 0;
    }
    
  }
  
  int pop(){
    if(this.cnt <= 0){ return -1; }
    else{ 
      this.data[this.f++] = 0;
      this.cnt--;
      if(this.f >= size){ this.f = 0; }
      return 0;
    }
  }
  
  int front(){
    if(this.cnt <= 0){ return -1; }
    else{ return this.data[this.f]; } 
  }
  
  int size(){
    return this.cnt;
  }
}
```