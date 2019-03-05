
# 구슬 탈출 2 

## 문제

스타트링크에서 판매하는 어린이용 장난감 중에서 가장 인기가 많은 제품은 구슬 탈출이다. 구슬 탈출은 직사각형 보드에 빨간 구슬과 파란 구슬을 하나씩 넣은 다음, 빨간 구슬을 구멍을 통해 빼내는 게임이다.

보드의 세로 크기는 N, 가로 크기는 M이고, 편의상 1×1크기의 칸으로 나누어져 있다. 가장 바깥 행과 열은 모두 막혀져 있고, 보드에는 구멍이 하나 있다. 빨간 구슬과 파란 구슬의 크기는 보드에서 1×1크기의 칸을 가득 채우는 사이즈이고, 각각 하나씩 들어가 있다. 게임의 목표는 빨간 구슬을 구멍을 통해서 빼내는 것이다. 이때, 파란 구슬이 구멍에 들어가면 안된다.

이때, 구슬을 손으로 건드릴 수는 없고, 중력을 이용해서 이리 저리 굴려야 한다. 왼쪽으로 기울이기, 오른쪽으로 기울이기, 위쪽으로 기울이기, 아래쪽으로 기울이기와 같은 네 가지 동작이 가능하다.

각각의 동작에서 공은 동시에 움직인다. 빨간 구슬이 구멍에 빠지면 성공이지만, 파란 구슬이 구멍에 빠지면 실패이다. 빨간 구슬과 파란 구슬이 동시에 구멍에 빠져도 실패이다. 빨간 구슬과 파란 구슬은 동시에 같은 칸에 있을 수 없다. 또, 빨간 구슬과 파란 구슬의 크기는 한 칸을 모두 차지한다. 기울이는 동작을 그만하는 것은 더 이상 구슬이 움직이지 않을 때 까지이다.

보드의 상태가 주어졌을 때, 최소 몇 번 만에 빨간 구슬을 구멍을 통해 빼낼 수 있는지 구하는 프로그램을 작성하시오.

## 입력

첫 번째 줄에는 보드의 세로, 가로 크기를 의미하는 두 정수 N, M (3 ≤ N, M ≤ 10)이 주어진다. 다음 N개의 줄에 보드의 모양을 나타내는 길이 M의 문자열이 주어진다. 이 문자열은 '`.`', '`#`', '`O`', '`R`', '`B`' 로 이루어져 있다. '`.`'은 빈 칸을 의미하고, '`#`'은 공이 이동할 수 없는 장애물 또는 벽을 의미하며, '`O`'는 구멍의 위치를 의미한다. '`R`'은 빨간 구슬의 위치, '`B`'는 파란 구슬의 위치이다.

입력되는 모든 보드의 가장자리에는 모두 '`#`'이 있다. 구멍의 개수는 한 개 이며, 빨간 구슬과 파란 구슬은 항상 1개가 주어진다.

## 출력

최소 몇 번 만에 빨간 구슬을 구멍을 통해 빼낼 수 있는지 출력한다. 만약, 10번 이하로 움직여서 빨간 구슬을 구멍을 통해 빼낼 수 없으면 -1을 출력한다.

## 예제 입력 1  복사

5 5
#####
#..B#
#.#.#
#RO.#
#####

## 예제 출력 1  복사

1

## 예제 입력 2  복사

7 7
#######
#...RB#
#.#####
#.....#
#####.#
#O....#
#######

## 예제 출력 2  복사

5

## 예제 입력 3  복사

7 7
#######
#..R#B#
#.#####
#.....#
#####.#
#O....#
#######

## 예제 출력 3  복사

5

## 예제 입력 4  복사

10 10
##########
#R#...##B#
#...#.##.#
#####.##.#
#......#.#
#.######.#
#.#....#.#
#.#.#.#..#
#...#.O#.#
##########

## 예제 출력 4  복사

-1

## 예제 입력 5  복사

3 7
#######
#R.O.B#
#######

## 예제 출력 5  복사

1

## 예제 입력 6  복사

10 10
##########
#R#...##B#
#...#.##.#
#####.##.#
#......#.#
#.######.#
#.#....#.#
#.#.##...#
#O..#....#
##########

## 예제 출력 6  복사

7

## 예제 입력 7  복사

3 10
##########
#.O....RB#
##########

## 예제 출력 7  복사

-1

## 출처

-   문제를 만든 사람:  [baekjoon](https://www.acmicpc.net/user/baekjoon)
-   잘못된 데이터를 찾은 사람:  [jason9319](https://www.acmicpc.net/user/jason9319)  [tncks0121](https://www.acmicpc.net/user/tncks0121)
-   데이터를 추가한 사람:  [kkw564](https://www.acmicpc.net/user/kkw564)
-   문제의 오타를 찾은 사람:  [sky1357](https://www.acmicpc.net/user/sky1357)  [welchsgrape](https://www.acmicpc.net/user/welchsgrape)  [wurikiji](https://www.acmicpc.net/user/wurikiji)
-   어색한 표현을 찾은 사람:  [toysmars](https://www.acmicpc.net/user/toysmars)

## 알고리즘 분류

-   [BFS](https://www.acmicpc.net/problem/tag/BFS)
-   [브루트 포스](https://www.acmicpc.net/problem/tag/%EB%B8%8C%EB%A3%A8%ED%8A%B8%20%ED%8F%AC%EC%8A%A4)

## 코드

```java
import java.util.StringTokenizer;
import java.io.IOException;
import java.io.BufferedReader;
import java.io.InputStreamReader;

import java.util.Queue;
import java.util.LinkedList;

public class Main {

	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		
		//N,M
		int N = Integer.parseInt(st.nextToken());
		int M = Integer.parseInt(st.nextToken());
		
		char matrix[][] = new char[N][M];
		int[][][][] visited = new int[N][M][N][M];
		Queue<MarbleState> q = new LinkedList<MarbleState>();
		
		int ri = 0, rj = 0, bi = 0, bj = 0;

		for(int i=0; i<N; i++) {
			String line = br.readLine();
			for(int j=0; j<M; j++) {
				char ch = line.charAt(j);
				matrix[i][j] = ch;
				if(ch == 'R') { ri = i; rj = j; }
				if(ch == 'B') { bi = i; bj = j; }
			}
		}
		
		//Init Queue
		q.offer(new MarbleState(ri,rj,bi,bj,0));
		visited[ri][rj][bi][bj] = 1;
		
		//BFS
		int res = BFS(q, matrix, visited);
		System.out.println(res);
	}
	
	public static int BFS(Queue<MarbleState> q, char[][] matrix, int[][][][] visited) {					
		int[] di = { -1, 1, 0, 0};
		int[] dj = {0, 0, -1, 1};
		
		int res = -1;
		
		while(!q.isEmpty()) {
			
			MarbleState cur = q.poll();
			int cur_ri = cur.ri;
			int cur_rj = cur.rj; 
			int cur_bi = cur.bi;
			int cur_bj = cur.bj;
			int cur_cnt = cur.cnt;
			
			//횟수가 10번 넘어가면 게임 중료 
			if(cur_cnt > 10) { break; }
			//빨간색 구슬만 구멍에 들어간 경우 현재 움직임 횟수 저장후 게임 종료  
			if(matrix[cur_ri][cur_rj] == 'O' && matrix[cur_bi][cur_bj] != 'O') { res = cur_cnt; break; }
			//파란색 구슬이 구멍에 먼저 들어가게 되면 종료 -> 이 코드를 넣게 되면 틀림!
			//왜? 모든 경우를 탐색하는 것이 아니기 때문에 
 			//if(matrix[cur_bi][cur_bj] == 'O') { break; }
			
			//위 2가지 경우가 아니면 상/하/좌/ 기울여서 새로운 상태 큐에 저장 
			for(int dir=0; dir<4; dir++) {
				int next_ri = cur_ri;
				int next_rj = cur_rj;
				int next_bi = cur_bi;
				int next_bj = cur_bj;
				
				
				//R 이동 
				while(true) {
					//옮겨진 자리가 벽(#), 구멍(O)이 아니라면 다음칸으로 칸으로 이동
					if(matrix[next_ri][next_rj] != '#' && matrix[next_ri][next_rj] != 'O') {
						next_ri += di[dir];
						next_rj += dj[dir];
					}else {
						//옮겨진 자리가 벽(#) 이라면, 벽에 위치할 수는 없으므로 한칸 전으로 이동시킨 후 멈춘다.
						if(matrix[next_ri][next_rj] == '#') {
							next_ri -= di[dir];
							next_rj -= dj[dir];
						}
						//옮겨진 자리가 구멍(O) 이라면, 자리 이동을 멈춘다. 
						break;						
					}
				}
				
				//B 이동 
				while(true) {
					//옮겨진 자리가 벽(#), 구멍(O)이 아니라면 다음칸으로 칸으로 이동
					if(matrix[next_bi][next_bj] != '#' && matrix[next_bi][next_bj] != 'O') {
						next_bi += di[dir];
						next_bj += dj[dir];
					}else {
						//옮겨진 자리가 벽(#) 이라면, 벽에 위치할 수는 없으므로 한칸 전으로 이동시킨 후 멈춘다.
						if(matrix[next_bi][next_bj] == '#') {
							next_bi -= di[dir];
							next_bj -= dj[dir];
						}
						//옮겨진 자리가 구멍(O) 이라면, 자리 이동을 멈춘다. 
						break;						
					}
				}				
				
				// R, B를 모두 한쪽으로 옮긴 후, 두 위치가 같은 경우 
				if(next_ri == next_bi && next_rj == next_bj) {
					// 구멍이 아닌경우에 
					if(matrix[next_ri][next_rj] != 'O') {
						//나중에 도착한 구슬을 한칸 이전에 배치
						int r_distance = Math.abs(next_ri - cur_ri) + Math.abs(next_rj - cur_rj);
						int d_distance = Math.abs(next_bi - cur_bi) + Math.abs(next_bj - cur_bj);
						
						if(r_distance < d_distance) {
							next_bi -= di[dir]; next_bj -= dj[dir];
						}else {
							next_ri -= di[dir]; next_rj -= dj[dir];
						}																			
					}					
				}
				
				//방문 기록 확하고 큐에 넣기
				if(visited[next_ri][next_rj][next_bi][next_bj] == 0) {
					visited[next_ri][next_rj][next_bi][next_bj] = 1;
					q.offer(new MarbleState(next_ri, next_rj, next_bi, next_bj, cur_cnt+1));
				}
				
			}
			
		} // while q end
		
		return res;
	}
	


}

class MarbleState{	
	int ri;
	int rj;
	int bi;
	int bj;
	int cnt;
		
	public MarbleState(int ri, int rj, int bi, int bj, int cnt) {
		this.ri = ri;
		this.rj = rj;
		this.bi = bi;
		this.bj = bj;
		this.cnt = cnt;
	}
	    
}

```