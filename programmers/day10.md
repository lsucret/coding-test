
Day 10 – BFS

게임 맵 최단거리 (Lv2) https://school.programmers.co.kr/learn/courses/30/lessons/1844

재귀로 풀려다가 실패ㅠ

DFS
- 깊이 우선 탐색
- 한 갈래로 끝까지 가고, 안되면 그 다음으로 감
- LIFO방식으로 탐색. 재귀나 스택으로 구현
- 모든 경우의 수 구할때 사용
BFS
- 너비 우선 탐색
- 단계별로 여러 갈래로 모두 가면서 탐색.
- FIFO 구조로 구현. Queue 사용.
- 최단거리 구할때 사용.


```java

import java.util.*;

class Solution {
    // 상, 하, 좌, 우
    private static final int[] dy = {-1, 1, 0, 0};
    private static final int[] dx = {0, 0, -1, 1};

    public int solution(int[][] maps) {
        int n = maps.length;
        int m = maps[0].length;

        boolean[][] visited = new boolean[n][m];
        Queue<int[]> q = new LinkedList<>();

        // y, x, distance
        q.offer(new int[]{0, 0, 1});
        visited[0][0] = true;

        while (!q.isEmpty()) {
            int[] cur = q.poll();
            int y = cur[0];
            int x = cur[1];
            int dist = cur[2];

            // 도착 지점에 처음 도달한 순간이 최단 거리
            if (y == n - 1 && x == m - 1) {
                return dist;
            }

            for (int dir = 0; dir < 4; dir++) {
                int ny = y + dy[dir];
                int nx = x + dx[dir];

                // 범위 체크
                if (ny < 0 || ny >= n || nx < 0 || nx >= m) {
                    continue;
                }
                // 벽이거나 이미 방문한 곳은 스킵
                if (maps[ny][nx] == 0 || visited[ny][nx]) {
                    continue;
                }

                visited[ny][nx] = true;
                System.out.println(dist+":"+ny+ nx);
                q.offer(new int[]{ny, nx, dist + 1});
            }
        }

        // 도달 불가
        return -1;
    }
}

```
