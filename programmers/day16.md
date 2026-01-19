
Day 16 – DFS 응용

단어 변환 (Lv3) https://school.programmers.co.kr/learn/courses/30/lessons/43163

```java

import java.util.*;

class Solution {
    public int solution(String begin, String target, String[] words) {
        int answer = 0;
        
        boolean[] visited = new boolean[words.length];
        Queue<int[]> q = new LinkedList<>(); // int배열 대신 Node란 객체를 만들어서 String, int를 넣어도 된다.
        q.offer(new int[]{-1, 0});
        while (!q.isEmpty()) {
            int[] cur = q.poll();
            String temp = (cur[0] == -1) ? begin : words[cur[0]];
            int dist = cur[1];
            
            if (temp.equals(target)) {
                return dist;
            }
            
            for (int i = 0; i < words.length; i++) {
                if (countDiff(temp, words[i]) == 1 && !visited[i]) {
                    visited[i] = true;
                    q.offer(new int[]{i, dist + 1});
                }
            }
        }
        return 0;
    }
    
    private int countDiff(String base, String compare) {
        int diff = 0;
        for (int i = 0; i < base.length(); i++) {
            if (base.charAt(i) != compare.charAt(i)) {
                diff++;
            }
        }
        return diff;
    }
    
}
```



AI 풀이
```java
import java.util.*;

class Solution {
    public int solution(String begin, String target, String[] words) {
        // target이 words에 없으면 변환 불가
        boolean exists = false;
        for (String w : words) {
            if (w.equals(target)) {
                exists = true;
                break;
            }
        }
        if (!exists) return 0;

        boolean[] visited = new boolean[words.length];
        Queue<Node> q = new ArrayDeque<>();
        q.offer(new Node(begin, 0));

        while (!q.isEmpty()) {
            Node cur = q.poll();
            String curWord = cur.word;
            int step = cur.step;

            if (curWord.equals(target)) {
                return step;
            }

            for (int i = 0; i < words.length; i++) {
                if (visited[i]) continue;
                if (diffOne(curWord, words[i])) {
                    visited[i] = true;
                    q.offer(new Node(words[i], step + 1));
                }
            }
        }

        return 0; // 끝까지 못 가면 불가능
    }

    // 두 단어가 정확히 한 글자만 다른지
    private boolean diffOne(String a, String b) {
        int diff = 0;
        for (int i = 0; i < a.length(); i++) {
            if (a.charAt(i) != b.charAt(i)) {
                diff++;
                if (diff > 1) return false;
            }
        }
        return diff == 1;
    }

    private static class Node {
        String word;
        int step;
        Node(String word, int step) {
            this.word = word;
            this.step = step;
        }
    }
}


```
