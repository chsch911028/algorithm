
# 시험 감독  성공

## 문제

총 N개의 시험장이 있고, 각각의 시험장마다 응시자들이 있다. i번 시험장에 있는 응시자의 수는 Ai명이다.

감독관은 총감독관과 부감독관으로 두 종류가 있다. 총감독관은 한 방에서 감시할 수 있는 응시자의 수가 B명이고, 부감독관은 한 방에서 감시할 수 있는 응시자의 수가 C명이다.

각각의 시험장에 총감독관은 오직 1명만 있어야 하고, 부감독관은 여러 명 있어도 된다.

각 시험장마다 응시생들을 모두 감시해야 한다. 이때, 필요한 감독관 수의 최솟값을 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 시험장의 개수 N(1 ≤ N ≤ 1,000,000)이 주어진다.

둘째 줄에는 각 시험장에 있는 응시자의 수 Ai  (1 ≤ Ai  ≤ 1,000,000)가 주어진다.

셋째 줄에는 B와 C가 주어진다. (1 ≤ B, C ≤ 1,000,000)

## 출력

각 시험장마다 응시생을 모두 감독하기 위해 필요한 감독관의 최소 수를 출력한다.

## 예제 입력 1  복사

1
1
1 1

## 예제 출력 1  복사

1

## 예제 입력 2  복사

3
3 4 5
2 2

## 예제 출력 2  복사

7

## 예제 입력 3  복사

5
1000000 1000000 1000000 1000000 1000000
5 7

## 예제 출력 3  복사

714290

## 예제 입력 4  복사

5
10 9 10 9 10
7 20

## 예제 출력 4  복사

10

## 예제 입력 5  복사

5
10 9 10 9 10
7 2

## 예제 출력 5  복사

13

## 출처

-   문제를 만든 사람:  [baekjoon](https://www.acmicpc.net/user/baekjoon)
-   문제의 오타를 찾은 사람:  [citizen](https://www.acmicpc.net/user/citizen)  [jhpark1109](https://www.acmicpc.net/user/jhpark1109)

## 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main {

	public static void main(String[] args) throws IOException {
		// TODO Auto-generated method stub
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));		
		
		int n = Integer.parseInt(br.readLine());
		int[] attendant = new int[n];
		StringTokenizer st = new StringTokenizer(br.readLine());
		StringTokenizer st2 = new StringTokenizer(br.readLine());
		int b = Integer.parseInt(st2.nextToken()); //총감독관
		int c = Integer.parseInt(st2.nextToken()); //부감독관
		
		long sum = n;
		for(int i=0; i<n; i++) {
			attendant[i] = Integer.parseInt(st.nextToken())-b;
			
			if(attendant[i] > 0) {				
				sum += attendant[i] / c;
				if(attendant[i]%c != 0) { sum++; }
			} 			
		}
		
		System.out.println(sum);		
	}

}
```