
Day 15 – DFS/BFS

네트워크 (Lv2) https://school.programmers.co.kr/learn/courses/30/lessons/43162

```java
/*
정확성  테스트
테스트 1 〉	통과 (0.02ms, 74.2MB)
테스트 2 〉	통과 (0.02ms, 74.7MB)
테스트 3 〉	통과 (0.02ms, 85.7MB)
테스트 4 〉	통과 (0.02ms, 79.7MB)
테스트 5 〉	통과 (0.01ms, 79.5MB)
테스트 6 〉	통과 (0.06ms, 80.5MB)
테스트 7 〉	통과 (0.02ms, 75.4MB)
테스트 8 〉	통과 (0.05ms, 86.9MB)
테스트 9 〉	통과 (0.05ms, 73.3MB)
테스트 10 〉	통과 (0.08ms, 90.6MB)
테스트 11 〉	통과 (0.28ms, 77.6MB)
테스트 12 〉	통과 (0.16ms, 75.3MB)
테스트 13 〉	통과 (0.14ms, 81MB)
*/
class Solution {
    public int solution(int n, int[][] computers) {
        boolean[] visited = new boolean[n];
        int networkCount = 0;

        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                dfs(i, computers, visited);
                networkCount++;
            }
        }

        return networkCount;
    }

    private void dfs(int node, int[][] computers, boolean[] visited) {
        visited[node] = true;

        for (int next = 0; next < computers.length; next++) {
            // 연결되어 있고, 아직 방문하지 않았다면 탐색
            if (computers[node][next] == 1 && !visited[next]) {
                dfs(next, computers, visited);
            }
        }
    }
}
```

```java
/*
정확성  테스트
테스트 1 〉	통과 (0.09ms, 89.1MB)
테스트 2 〉	통과 (0.08ms, 69.7MB)
테스트 3 〉	통과 (0.11ms, 86.9MB)
테스트 4 〉	통과 (0.13ms, 80.6MB)
테스트 5 〉	통과 (0.01ms, 91.6MB)
테스트 6 〉	통과 (0.30ms, 84.2MB)
테스트 7 〉	통과 (0.12ms, 87MB)
테스트 8 〉	통과 (0.23ms, 84.3MB)
테스트 9 〉	통과 (0.17ms, 91.6MB)
테스트 10 〉	통과 (0.28ms, 79.5MB)
테스트 11 〉	통과 (0.69ms, 89.2MB)
테스트 12 〉	통과 (0.73ms, 87MB)
테스트 13 〉	통과 (0.31ms, 76.4MB)
*/
import java.util.*;
class Solution {
    public int solution(int n, int[][] computers) {
        if (n == 1) return 1;

        int answer = 0;
        Set<Integer> idx = new HashSet();
        for (int k = 0; k < n; k++) {
            idx.add(k);
        }
        
        while(idx.iterator().hasNext()) { // Set을 변경하면서 iterator를 순회하는 것을 위험하다!Iterator는 내부 값이 변경되면 동시성 에러를 뱉는다. (ConcurrentModificationException)
        answer++;
        dfs(computers, idx, idx.iterator().next());
        }
        
        return answer;
    }
    
    private void dfs(int[][] computers, Set<Integer> idx, int i) {
        if (!idx.contains(i)) {
            return;
        }
        for (int j = 0; j < computers.length; j++) {
            int connect = computers[i][j];
            if (connect == 1) {
                idx.remove(i);
                dfs(computers, idx, j);
                idx.remove(j);
            }
        }
    }
    
}
```
