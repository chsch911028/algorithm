# 연구소

## 문제

인체에 치명적인 바이러스를 연구하던 연구소에서 바이러스가 유출되었다. 다행히 바이러스는 아직 퍼지지 않았고, 바이러스의 확산을 막기 위해서 연구소에 벽을 세우려고 한다.

연구소는 크기가 N×M인 직사각형으로 나타낼 수 있으며, 직사각형은 1×1 크기의 정사각형으로 나누어져 있다. 연구소는 빈 칸, 벽으로 이루어져 있으며, 벽은 칸 하나를 가득 차지한다.

일부 칸은 바이러스가 존재하며, 이 바이러스는 상하좌우로 인접한 빈 칸으로 모두 퍼져나갈 수 있다. 새로 세울 수 있는 벽의 개수는 3개이며, 꼭 3개를 세워야 한다.

예를 들어, 아래와 같이 연구소가 생긴 경우를 살펴보자.

2 0 0 0 1 1 0
0 0 1 0 1 2 0
0 1 1 0 1 0 0
0 1 0 0 0 0 0
0 0 0 0 0 1 1
0 1 0 0 0 0 0
0 1 0 0 0 0 0

이때, 0은 빈 칸, 1은 벽, 2는 바이러스가 있는 곳이다. 아무런 벽을 세우지 않는다면, 바이러스는 모든 빈 칸으로 퍼져나갈 수 있다.

2행 1열, 1행 2열, 4행 6열에 벽을 세운다면 지도의 모양은 아래와 같아지게 된다.

2 1 0 0 1 1 0
1 0 1 0 1 2 0
0 1 1 0 1 0 0
0 1 0 0 0 1 0
0 0 0 0 0 1 1
0 1 0 0 0 0 0
0 1 0 0 0 0 0

바이러스가 퍼진 뒤의 모습은 아래와 같아진다.

2 1 0 0 1 1 2
1 0 1 0 1 2 2
0 1 1 0 1 2 2
0 1 0 0 0 1 2
0 0 0 0 0 1 1
0 1 0 0 0 0 0
0 1 0 0 0 0 0

벽을 3개 세운 뒤, 바이러스가 퍼질 수 없는 곳을 안전 영역이라고 한다. 위의 지도에서 안전 영역의 크기는 27이다.

연구소의 지도가 주어졌을 때 얻을 수 있는 안전 영역 크기의 최댓값을 구하는 프로그램을 작성하시오.

## 입력

첫째 줄에 지도의 세로 크기 N과 가로 크기 M이 주어진다. (3 ≤ N, M ≤ 8)

둘째 줄부터 N개의 줄에 지도의 모양이 주어진다. 0은 빈 칸, 1은 벽, 2는 바이러스가 있는 위치이다. 2의 개수는 2보다 크거나 같고, 10보다 작거나 같은 자연수이다.

빈 칸의 개수는 3개 이상이다.

## 출력

첫째 줄에 얻을 수 있는 안전 영역의 최대 크기를 출력한다.

## 예제 입력 1 복사

7 7
2 0 0 0 1 1 0
0 0 1 0 1 2 0
0 1 1 0 1 0 0
0 1 0 0 0 0 0
0 0 0 0 0 1 1
0 1 0 0 0 0 0
0 1 0 0 0 0 0

## 예제 출력 1 복사

27

## 예제 입력 2 복사

4 6
0 0 0 0 0 0
1 0 0 0 0 2
1 1 1 0 0 2
0 0 0 0 0 2

## 예제 출력 2 복사

9

## 예제 입력 3 복사

8 8
2 0 0 0 0 0 0 2
2 0 0 0 0 0 0 2
2 0 0 0 0 0 0 2
2 0 0 0 0 0 0 2
2 0 0 0 0 0 0 2
0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0

## 예제 출력 3 복사

3

## 출처

- 문제를 만든 사람: [baekjoon](https://www.acmicpc.net/user/baekjoon)
- 빠진 조건을 찾은 사람: [bupjae](https://www.acmicpc.net/user/bupjae) [dotorya](https://www.acmicpc.net/user/dotorya)

## 코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;

import java.util.Queue;
import java.util.LinkedList;


public class Laboratory {

    static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    static int n;
    static int m;
    static int map[][];
    static int res = 0;
    static int[] dy = {-1, 1, 0, 0};
    static int[] dx = {0, 0, -1, 1};

    public static void main(String[] args) throws IOException {

        String[] input = br.readLine().split(" ");
        n = Integer.parseInt(input[0]);
        m = Integer.parseInt(input[1]);

        map = new int[n][m];

        //set map
        for (int y = 0; y < n; y++) {
            String[] line = br.readLine().split(" ");
            for (int x = 0; x < m; x++) {
                map[y][x] = Integer.parseInt(line[x]);
            }
        }

        /*
         * 풀이방법
         *
         * 1. dfs(백트랙킹)로 빈칸(0)에 3개의 벽을 설치하는 모든 경우를 탐색한다.
         * 2. bfs로 바이러스(2)가 상하좌우로 확장시킨후 남아있는 빈칸(안전지역)의 갯수를 결정한다.
         *
         * */

        dfs(0, 0, 0);

        System.out.println(res);
    }

    public static void dfs(int count, int sy, int sx) {
        if (count == 3) {
            bfs();
            return;
        }

        for (int y = sy; y < n; y++) {
            for (int x = sx; x < m; x++) {
                if (map[y][x] == 0) {
                    map[y][x] = 1;
                    dfs(count + 1, y, x);
                    map[y][x] = 0;
                }
            }
            sx = 0;
        }
    }

    public static void bfs() {
        Queue<Integer> q = new LinkedList<Integer>();
        int backup[][] = new int[n][m];
        int visited[][] = new int[n][m];

        for (int y = 0; y < n; y++) {
            for (int x = 0; x < m; x++) {
                backup[y][x] = map[y][x];
                if (backup[y][x] == 2) {
                    //y,x 좌표를 한번에 구할 수 있도록 하는 방법(y*10 + x)
                    q.offer((y * 10) + x);
                    visited[y][x] = 1;
                }
            }
        }

        while (!q.isEmpty()) {
            int cur = q.poll();
            int y = cur / 10;
            int x = cur % 10;

            backup[y][x] = 2;

            for (int dir = 0; dir < 4; dir++) {
                int ny = y + dy[dir];
                int nx = x + dx[dir];

                if (ny < 0 || ny >= n || nx < 0 || nx >= m) {
                    continue;
                }

                if (visited[ny][nx] == 0 && backup[ny][nx] == 0) {
                    visited[ny][nx] = 1;
                    q.offer((ny * 10) + nx);
                }
            }

        }

        int safeCnt = 0;
        for (int y = 0; y < n; y++) {
            for (int x = 0; x < m; x++) {
                if (backup[y][x] == 0) {
                    safeCnt++;
                }
            }
        }

        if (res < safeCnt) {
            res = safeCnt;
        }
    }
}

```
