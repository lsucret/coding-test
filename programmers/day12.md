
Day 12 – 힙

더 맵게 (Lv2) https://school.programmers.co.kr/learn/courses/30/lessons/42626

```java
import java.util.*;

class Solution {
    public int solution(int[] scoville, int K) {
        Queue<Integer> q = new PriorityQueue<Integer>();
        
        for (int score : scoville) {
            q.offer(score);
        }

        while (K > q.peek() && q.size() >= 2) {
            Integer num1 = q.poll();
            Integer num2 = q.poll();
            q.offer(shake(num1, num2));
        }
        
        return (K > q.peek()) ? -1 : scoville.length - q.size();
    }
    
    private Integer shake(Integer num1, Integer num2) {
        return num1 + (num2 * 2);
    }
}
```
