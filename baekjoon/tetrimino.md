# 테트로미노 성공

## 문제

폴리오미노란 크기가 1×1인 정사각형을 여러 개 이어서 붙인 도형이며, 다음과 같은 조건을 만족해야 한다.

- 정사각형은 서로 겹치면 안된다.
- 도형은 모두 연결되어 있어야 한다.
- 정사각형의 꼭짓점끼리 연결되어 있어야 한다. 즉, 변과 꼭짓점이 맞닿아있으면 안된다.

정사각형 4개를 이어 붙인 폴리오미노는 테트로미노라고 하며, 다음과 같은 5가지가 있다.

![tetrimino](tetrimino.png)

아름이는 크기가 N×M인 종이 위에 테트로미노 하나를 놓으려고 한다. 종이는 1×1 크기의 칸으로 나누어져 있으며, 각각의 칸에는 정수가 하나 쓰여 있다.

테트로미노 하나를 적절히 놓아서 테트로미노가 놓인 칸에 쓰여 있는 수들의 합을 최대로 하는 프로그램을 작성하시오.

테트로미노는 반드시 한 정사각형이 정확히 하나의 칸을 포함하도록 놓아야 하며, 회전이나 대칭을 시켜도 된다.

## 입력

첫째 줄에 종이의 세로 크기 N과 가로 크기 M이 주어진다. (4 ≤ N, M ≤ 500)

둘째 줄부터 N개의 줄에 종이에 쓰여 있는 수가 주어진다. i번째 줄의 j번째 수는 위에서부터 i번째 칸, 왼쪽에서부터 j번째 칸에 쓰여 있는 수이다. 입력으로 주어지는 수는 1,000을 넘지 않는 자연수이다.

## 출력

첫째 줄에 테트로미노가 놓인 칸에 쓰인 수들의 합의 최댓값을 출력한다.

## 예제 입력 1 복사

5 5
1 2 3 4 5
5 4 3 2 1
2 3 4 5 6
6 5 4 3 2
1 2 1 2 1

## 예제 출력 1 복사

19

## 예제 입력 2 복사

4 5
1 2 3 4 5
1 2 3 4 5
1 2 3 4 5
1 2 3 4 5

## 예제 출력 2 복사

20

## 예제 입력 3 복사

4 10
1 2 1 2 1 2 1 2 1 2
2 1 2 1 2 1 2 1 2 1
1 2 1 2 1 2 1 2 1 2
2 1 2 1 2 1 2 1 2 1

## 예제 출력 3 복사

7

## 출처

- 문제를 만든 사람: [baekjoon](https://www.acmicpc.net/user/baekjoon)
- 데이터를 추가한 사람: [stack](https://www.acmicpc.net/user/stack) [vjerksen](https://www.acmicpc.net/user/vjerksen)

## 코드

```java
package test;

import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.StringTokenizer;
import java.io.IOException;


public class Tetrimino {

	public static int model[][][] = {

			{
				{1,0,0,0},
				{1,0,0,0},
				{1,0,0,0},
				{1,0,0,0}
			},

			{
				{1,1,1,1},
				{0,0,0,0},
				{0,0,0,0},
				{0,0,0,0}
			},

			{
				{1,1,1,0},
				{0,0,1,0},
				{0,0,0,0},
				{0,0,0,0}
			},

			{
				{1,1,1,0},
				{1,0,0,0},
				{0,0,0,0},
				{0,0,0,0}
			},

			{
				{0,0,1,0},
				{1,1,1,0},
				{0,0,0,0},
				{0,0,0,0}
			},

			{
				{1,0,0,0},
				{1,1,1,0},
				{0,0,0,0},
				{0,0,0,0}
			},

			{
				{0,1,0,0},
				{0,1,0,0},
				{1,1,0,0},
				{0,0,0,0}
			},

			{
				{1,0,0,0},
				{1,0,0,0},
				{1,1,0,0},
				{0,0,0,0}
			},

			{
				{1,1,0,0},
				{1,0,0,0},
				{1,0,0,0},
				{0,0,0,0}
			},

			{
				{1,1,0,0},
				{0,1,0,0},
				{0,1,0,0},
				{0,0,0,0}
			},


			{
				{1,0,0,0},
				{1,1,0,0},
				{0,1,0,0},
				{0,0,0,0}
			},

			{
				{0,1,0,0},
				{1,1,0,0},
				{1,0,0,0},
				{0,0,0,0}
			},

			{
				{1,1,0,0},
				{0,1,1,0},
				{0,0,0,0},
				{0,0,0,0}
			},

			{
				{0,1,1,0},
				{1,1,0,0},
				{0,0,0,0},
				{0,0,0,0}
			},

			{
				{1,0,0,0},
				{1,1,0,0},
				{1,0,0,0},
				{0,0,0,0}
			},

			{
				{1,1,1,0},
				{0,1,0,0},
				{0,0,0,0},
				{0,0,0,0}
			},

			{
				{0,1,0,0},
				{1,1,0,0},
				{0,1,0,0},
				{0,0,0,0}
			},

			{
				{0,1,0,0},
				{1,1,1,0},
				{0,0,0,0},
				{0,0,0,0}
			},

			{
				{1,1,0,0},
				{1,1,0,0},
				{0,0,0,0},
				{0,0,0,0}
			}
	};


	public static void main(String[] args) throws IOException {
		// TODO Auto-generated method stub
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());

		int N = Integer.parseInt(st.nextToken());
		int M = Integer.parseInt(st.nextToken());


		int map[][] = new int[N][M];
		for(int y=0; y<N; y++) {
			String[] line = br.readLine().split(" ");
			for(int x=0; x<M; x++) {
				map[y][x] = Integer.parseInt(line[x]);
			}
		}


		int max = 0;
		for(int y=0; y<N; y++) {
			for(int x=0; x<M; x++) {
				int cnt = getCount(y,x,N,M,map);
				if(cnt> max) { max = cnt;}
			}
		}

		System.out.println(max);

	}

	public static int getCount(int sy, int sx, int N, int M, int[][] map) {
		int max = 0;

		for(int i=0; i<19; i++) {
			int m[][] = model[i];
			int sum = 0;
			for(int y=0; y<4; y++) {
				for(int x=0; x<4; x++) {
					if(sx+x >= M || sy+y >= N) { continue; }
					if(m[y][x] == 1) { sum += map[sy+y][sx+x]; }
				}
			}
			if(sum > max) { max = sum;}
		}
		return max;
	}

}

```
