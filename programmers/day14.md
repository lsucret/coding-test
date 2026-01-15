
Day 14 – 종합

주식가격 (Lv2) https://school.programmers.co.kr/learn/courses/30/lessons/42584

## PriorityQueue
```java
/*
효율성  테스트
테스트 1 〉	통과 (83.93ms, 75.9MB)
테스트 2 〉	통과 (62.11ms, 74.3MB)
테스트 3 〉	통과 (88.73ms, 79.3MB)
테스트 4 〉	통과 (77.88ms, 76.7MB)
테스트 5 〉	통과 (56.71ms, 71.8MB)
*/
import java.util.Comparator;
import java.util.HashMap;
import java.util.Map;
import java.util.PriorityQueue;
import java.util.*;

class Solution {
    public int[] solution(int[] prices) {
        int[] answer = new int[prices.length];
        
        Queue<Map.Entry<Integer, Integer>> q = new PriorityQueue(
            Map.Entry.comparingByKey(Comparator.reverseOrder())
        );
        for (int i = 0; i < prices.length; i++) {
            final int nowPrice = prices[i];

            q.offer(Map.entry(nowPrice, i));
            answer[i] = prices.length - i - 1;
            
            while (!q.isEmpty() && q.peek().getKey() > nowPrice) {
                int idx = q.poll().getValue();
                answer[idx] = i - idx;
            }
        }

        return answer;
    }

}
```

```java
/*
효율성  테스트
테스트 1 〉	통과 (32.11ms, 73.9MB)
테스트 2 〉	통과 (24.48ms, 65.8MB)
테스트 3 〉	통과 (33.12ms, 73.9MB)
테스트 4 〉	통과 (28.63ms, 68.7MB)
테스트 5 〉	통과 (31.01ms, 70.4MB)
*/
import java.util.*;

class Solution {
    public int[] solution(int[] prices) {
        int[] answer = new int[prices.length];
        
        Stack<Integer> stack = new Stack();
        
        for (int i = 0; i < prices.length; i++) {
            final int nowPrice = prices[i];

            while (!stack.isEmpty() && prices[stack.peek()] > nowPrice) {
                int beforeIdx = stack.pop();
                answer[beforeIdx] = i - beforeIdx;
            }
            
            stack.push(i);
        }
        while (!stack.isEmpty()) {
            Integer idx = stack.pop();
            answer[idx] = prices.length - 1 - idx;
        }

        return answer;
    }

}

```


