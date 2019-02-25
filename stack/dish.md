# 접시

### 문제

----------

접시가 a, b, c, d 가 있고, 알파벳 순으로 한쪽이 막혀 있는 세척기에 들어간다고 할 때, b a c d 순으로 꺼내기 위해서는 push, push, pop, pop, push, pop, push, pop을 하면 된다. 세척기에서 꺼내는 순서가 주어질 때 그 동작을 출력하는 프로그램을 작성하시오. 만약 주어진 순서대로 접시를 꺼낼 수 없다면 “impossible”을 출력한다.

### 입력

----------

첫째 줄에 소문자 알파벳이 주어진다. 중복된 소문자 알파벳은 입력되지 않는다. 알파벳 소문자는 26개이다.

### 출력

----------

접시를 꺼내는 것이 가능한 경우 push, pop의 순서를 출력한다. 이것이 불가능하다면 impossible을 출력한다.

### 예제 입력

```
bacd
```

### 예제 출력

```
push
push
pop
pop
push
pop
push
pop
```

### 예제 입력

```
dabc
```

### 예제 출력

```
impossible
```


### 코드

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){

      // Please Enter Your Code Here
      Scanner sc = new Scanner(System.in);
      String str = sc.nextLine();
      int n = str.length();
      Stack stack = new Stack(n);
      
      //97 ~ 122
      int i = 0;
      int value = 97;
      boolean impossible = false;
      String opStr = "";
      
      while(i<n){
        int top = stack.top();
        if(top < 0){
          int res = stack.push(value++);
          if(res < 0){ impossible=true; break; }
          opStr = opStr + "push ";
        }else{
          char c = str.charAt(i);
          if(top == (int)c){ 
            stack.pop();
            opStr = opStr + "pop ";
            i++;
          }else{
            int res = stack.push(value++);
            if(res < 0){ impossible=true; break; }
            opStr = opStr + "push ";            
          }
        }
      }// while end
      
      if(impossible){
        System.out.println("impossible");
      }else{
        String ops[] = opStr.split(" ");
        for(int a=0; a<ops.length; a++){
          System.out.println(ops[a]);
        }
      }
      
    }
    
}




class Stack{
  int size;
  int data[];
  int len;
  
  public Stack(int size){
    this.size = size;
    this.data = new int[size];
    this.len = 0;
  }
  
  int push(int x){
    //overflow
    if(this.len >= this.size){ return -1;  }
    else{ this.data[this.len++] = x; return 0; }
  }  
  
  int pop(){
    //underflow 
    if(this.len-1 < 0){ return -1; }
    else{ this.len--; return this.data[this.len];   }
  }
  
  int top(){
    if(this.len-1 < 0){
      return -1;
    }else{
      int value = this.data[this.len-1];
      return value;
    }
  }
  
}
```