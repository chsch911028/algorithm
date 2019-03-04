
# 봄버맨 

## 문제

"봄버맨"은 크기가 R×C인 직사각형 격자판 위에서 살고 있다. 격자의 각 칸은 비어있거나 폭탄이 들어있다.

폭탄이 있는 칸은 3초가 지난 후에 폭발하고, 폭탄이 폭발한 이후에는 폭탄이 있던 칸이 파괴되어 빈 칸이 되며, 인접한 네 칸도 함께 파괴된다. 즉, 폭탄이 있던 칸이 (i, j)인 경우에 (i+1, j), (i-1, j), (i, j+1), (i, j-1)도 함께 파괴된다. 만약, 폭탄이 폭발했을 때, 인접한 칸에 폭탄이 있는 경우에는 인접한 폭탄은 폭발 없이 파괴된다. 따라서, 연쇄 반응은 없다.

봄버맨은 폭탄에 면역력을 가지고 있어서, 격자판의 모든 칸을 자유롭게 이동할 수 있다. 봄버맨은 다음과 같이 행동한다.

-   가장 처음에 봄버맨은 일부 칸에 폭탄을 설치해 놓는다. 모든 폭탄이 설치된 시간은 같다.
-   다음 1초 동안 봄버맨은 아무것도 하지 않는다.
-   다음 1초 동안 폭탄이 설치되어 있지 않은 모든 칸에 폭탄을 설치한다. 즉, 모든 칸은 폭탄을 가지고 있게 된다. 폭탄은 모두 동시에 설치했다고 가정한다.
-   1초가 지난 후에 3초 전에 설치된 폭탄이 모두 폭발한다.
-   3과 4를 반복한다.

폭탄을 설치해놓은 초기 상태가 주어졌을 때, N초가 흐른 후의 격자판 상태를 구하려고 한다.

예를 들어, 초기 상태가 아래와 같은 경우를 보자.

...
.O.
...

1초가 지난 후에는 아무 일도 벌어지지 않기 때문에, 위와 같다고 볼 수 있다. 1초가 더 흐른 후에 격자판의 상태는 아래와 같아진다.

OOO
OOO
OOO

1초가 지난 후엔 가운데에 있는 폭탄이 폭발해 가운데 칸과 인접한 네 칸이 빈 칸이 된다.

O.O
...
O.O

## 입력

첫째 줄에 R, C, N (1 ≤ R, C, N ≤ 200)이 주어진다. 둘째 줄부터 R개의 줄에 격자판의 초기 상태가 주어진다. 빈 칸은 '`.`'로, 폭탄은 '`O`'로 주어진다.

## 출력

총 R개의 줄에 N초가 지난 후의 격자판 상태를 출력한다.

## 예제 입력 1  복사

6 7 3
.......
...O...
....O..
.......
OO.....
OO.....

## 예제 출력 1  복사

OOO.OOO
OO...OO
OOO...O
..OO.OO
...OOOO
...OOOO

## 예제 입력 2  복사

6 7 4
.......
...O...
....O..
.......
OO.....
OO.....

## 예제 출력 2  복사

OOOOOOO
OOOOOOO
OOOOOOO
OOOOOOO
OOOOOOO
OOOOOOO

## 예제 입력 3  복사

6 7 5
.......
...O...
....O..
.......
OO.....
OO.....

## 예제 출력 3  복사

.......
...O...
....O..
.......
OO.....
OO.....

## 출처

-   문제를 번역한 사람:  [baekjoon](https://www.acmicpc.net/user/baekjoon)

## 코드1(Brute Force)

```java
import java.util.StringTokenizer;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;



public class Main {

	public static void main(String[] args) throws IOException{
		
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		
		int R = Integer.parseInt(st.nextToken());
		int C = Integer.parseInt(st.nextToken());
		int N = Integer.parseInt(st.nextToken());
		
		int[][] matrix = new int[R][C];
		
		//Init Matrix
		for(int i=0; i<R; i++) {
			String str = br.readLine();			
			for(int j=0; j<C; j++) {				
				if(str.charAt(j) == '.'){
					matrix[i][j] =  0; // 빈칸 = 0
				}else {
					matrix[i][j] =  3; // 폭탄 = 터칠시간 
				}				
			}
		}
		
		//Matrix Update
		for(int t=2; t<=N; t++) {
			if(t%2 == 0) { // 설치하는 타임 
				for(int i=0; i<R; i++) {
					for(int j=0; j<C; j++) {
						if(matrix[i][j] == 0) { //빈칸인경
							matrix[i][j] = t+3;
						}
					}
				}
			}else { // 터지는 타임 
				for(int i=0; i<R; i++) {
					for(int j=0; j<C; j++) {
						if(matrix[i][j] == t) {
							//자신 
							matrix[i][j] = 0;
							//상
							if(i-1 >= 0 && matrix[i-1][j] != t) { matrix[i-1][j] = 0;}							
							//하
							if(i+1 < R && matrix[i+1][j] != t) {matrix[i+1][j] = 0;}							
							//좌
							if(j-1 >= 0 && matrix[i][j-1] != t) {matrix[i][j-1] = 0;}							
							//우
							if(j+1 < C && matrix[i][j+1] != t) {matrix[i][j+1] = 0;}							
						
						}
					}
				}				
			}
			
		}// for t end		
		
		//Output Current Matrix
		for(int i=0; i<R; i++) {			
			for(int j=0; j<C; j++) {
				if(matrix[i][j] == 0) {
					System.out.print(".");
				}else {
					System.out.print("O");
				}								
			}
			System.out.println("");
		}				
		
	}

}
```

## 코드2 (BFS)

```java
import java.util.Queue;
import java.util.LinkedList;

import java.util.StringTokenizer;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.io.IOException;

public class Main {

	public static void main(String[] args) throws IOException {
		
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		
		int R = Integer.parseInt(st.nextToken());
		int C = Integer.parseInt(st.nextToken());
		int N = Integer.parseInt(st.nextToken());		
		
		int[][] matrix = new int[R][C];		 
		Queue<Bomb> q = new LinkedList<Bomb>();
		
		//Init Matrix
		initMatrix(R,C,matrix,q,br);
				
		//Matrix Update
		for(int t=2; t<=N; t++) {
			// 설치하는 타임
			if(t%2 == 0) { setBomb(R,C,matrix,q,t); }
			// 터지는 타임 
			else { doBomb(R,C,matrix,q,t); }			
		}// for t end		
		
		//Output Current Matrix
		for(int i=0; i<R; i++) {			
			for(int j=0; j<C; j++) {
				if(matrix[i][j] == 0) {
					System.out.print(".");
				}else {
					System.out.print("O");
				}
								
			}
			System.out.println("");
		}
				
	}

	public static void initMatrix(int R, int C, int[][] matrix, Queue<Bomb> q, BufferedReader br) throws IOException {
		for(int i=0; i<R; i++) {
			String str = br.readLine();		
			for(int j=0; j<C; j++) {				
				if(str.charAt(j) != '.'){
					Bomb obj = new Bomb(i,j,3);
					q.offer(obj);
					matrix[i][j] =  3; // 폭탄 = 터칠시간 
				}				
			}
		}
	}
	
	public static void setBomb(int R, int C, int[][] matrix, Queue<Bomb> q, int t) {
		for(int i=0; i<R; i++) {
			for(int j=0; j<C; j++) {
				if(matrix[i][j] == 0) { //빈칸인경
					Bomb obj = new Bomb(i,j,t+3);
					q.offer(obj);
					matrix[i][j] = t+3;
				}
			}
		}
	}
	
	public static void doBomb(int R, int C, int[][] matrix, Queue<Bomb> q, int t) {
		//top,bottom,left,right;
		int[] di = { -1, 1, 0, 0 };
		int[] dj = { 0, 0, -1, 1 };
		
		int size = q.size();
		while(size-- > 0) {			
			Bomb obj = q.poll();			
			//자신 빈칸 만들기
			int i = obj.i;
			int j = obj.j;
			int obj_t = obj.t;
			//이미 폭탄자격이 없어진 경우 패스
			if(matrix[i][j] == 0) { continue;}
			// 폭탄자격있는 친구만 다시 큐에 추가 
			if(obj_t != t) { q.offer(obj); continue; }
			// 터져야되는 친구는 주변과 함께 터지기 
			matrix[i][j] = 0;
			//상하좌우
			for(int n=0; n<4; n++) {
				int ni = i + di[n];
				int nj = j + dj[n];
				
				if(ni < 0 || ni >= R || nj < 0 || nj >= C) { continue; }
				if(matrix[ni][nj] == t) { continue; }
				matrix[ni][nj] = 0;
			}
		}
	}

}

class Bomb{
	int i;
	int j;
	int t;
	
	public Bomb(int i, int j, int t) {
		this.i = i;
		this.j = j;
		this.t = t;
	}
	
}
```

## 느끼점

<Brute Force 와 BFS> 2가지 개념으로 풀어봤다. 이 문제에서는 BFS를 이용해 풀더라도 어차피 2중 For문을 이용한 것과 동일한 만큼 탐색이 이루어지기 때문에, 속도면에서 더 빠른 결과를 얻지 못했다.  오히려 Queue를 사용하면서 생기는 추가작업 때문인지, 속도가 더 느린 결과가 나왔다.