
# 양념 반 후라이드 반  성공

## 문제

현진 치킨에서 판매하는 치킨은 양념 치킨, 후라이드 치킨, 반반 치킨으로 총 세 종류이다. 반반 치킨은 절반은 양념 치킨, 절반은 후라이드 치킨으로 이루어져있다. 양념 치킨 한 마리의 가격은 A원, 후라이드 치킨 한 마리의 가격은 B원, 반반 치킨 한 마리의 가격은 C원이다.

상도는 오늘 파티를 위해 양념 치킨 최소 X마리, 후라이드 치킨 최소 Y마리를 구매하려고 한다. 반반 치킨을 두 마리 구입해 양념 치킨 하나와 후라이드 치킨 하나를 만드는 방법도 가능하다. 상도가 치킨을 구매하는 금액의 최솟값을 구해보자.

## 입력

첫째 줄에 다섯 정수 A, B, C, X, Y가 주어진다.

## 출력

양념 치킨 최소 X마리, 후라이드 치킨 최소 Y마리를 구매하는 비용의 최솟값을 출력한다.

## 제한

-   1 ≤ A, B, C ≤ 5,000
-   1 ≤ X, Y ≤ 100,000

## 예제 입력 1  복사

1500 2000 1600 3 2

## 예제 출력 1  복사

7900

반반 치킨 4마리를 구매해서, 양념 치킨 2마리와 후라이드 치킨 2마리를 만들고, 양념 치킨 1마리를 구매하는 것이 최소이다.

## 예제 입력 2  

1500 2000 1900 3 2

## 예제 출력 2  

8500

## 예제 입력 3  

1500 2000 500 90000 100000

## 예제 출력 3  

100000000

## 출처

-   문제를 번역한 사람:  [baekjoon](https://www.acmicpc.net/user/baekjoon)


## 코드

```java
import java.util.StringTokenizer;
import java.io.IOException;
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class Main {

	public static void main(String[] args) throws IOException {
		BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(bf.readLine());
		
		int a = Integer.parseInt(st.nextToken());
		int b = Integer.parseInt(st.nextToken());
		int c = Integer.parseInt(st.nextToken());
		
		int x = Integer.parseInt(st.nextToken());
		int y = Integer.parseInt(st.nextToken());
		
        int gt_cnt = x > y ? x : y;
        int min_value = c*gt_cnt*2;
        
        if(c*2 <= a+b) {
        	int less_cnt = x < y ? x : y;
        	int banban_cnt = less_cnt*2;        	        	        	
        	int value = (banban_cnt*c)+(x-less_cnt)*a + (y-less_cnt)*b;
 
        	if(value < min_value) { min_value = value; }        	
        }else {
        	int value = x*a + y*b;
        	if(value < min_value) { min_value = value; }
        }
        	
        System.out.println(min_value);
	}
}
```