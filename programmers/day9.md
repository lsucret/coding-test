
Day 9 – DFS

타겟 넘버 (Lv2) https://school.programmers.co.kr/learn/courses/30/lessons/43165

// class 생성 (느림)
```java
import java.util.*;

class Solution {
    public int solution(int[] numbers, int target) {
        Current c = new Current(0, numbers);
        return c.getCount(target);
    }
    
    class Current {
        private final int sum; // 0
        private final int[] remain; // {1, 1, 1, 1, 1}
        Current (int sum, int[] remain) {
            this.sum = sum;
            this.remain = remain;
        }
        
        public boolean isEmptyRemain() {
            return remain == null;
        }
        
        public boolean needContinue(int target) {
            return Math.abs(sum - target) <= Arrays.stream(remain).sum();
        }
        
        public int getCount(int target) {
            if (isEmptyRemain()) {
                return sum == target ? 1 : 0;
            }
            if (needContinue(target)) {
                int[] nextRemain = (remain.length <= 1) ? null : Arrays.copyOfRange(remain, 1, remain.length);
                Current plus = new Current(sum + remain[0], nextRemain);
                Current minus = new Current(sum - remain[0], nextRemain);
                return plus.getCount(target) + minus.getCount(target);
            } else {
                return 0;                
            }
        }        
    }

}
```

```java
/*
테스트 1 〉	통과 (4.75ms, 80.8MB)
테스트 2 〉	통과 (7.67ms, 80.5MB)
테스트 3 〉	통과 (0.21ms, 90.7MB)
테스트 4 〉	통과 (0.40ms, 86.1MB)
테스트 5 〉	통과 (0.84ms, 90.8MB)
테스트 6 〉	통과 (0.45ms, 86.5MB)
테스트 7 〉	통과 (0.20ms, 84.3MB)
테스트 8 〉	통과 (0.39ms, 92.2MB)
*/
class Solution {
    public int solution(int[] numbers, int target) {

        return dfs(numbers, target, 0, 0);
    }

    public int dfs(int[] numbers, int target, int sum, int idx) {
        if (numbers.length == idx) {
            return (sum == target) ? 1 : 0;
        }
        return dfs(numbers, target, sum + numbers[idx], idx+1)
            + dfs(numbers, target, sum - numbers[idx], idx+1);
    }

}
```

중도 그만두기. (오히려 성능이 나빠짐.)
```java
import java.util.*;
/*
테스트 1 〉	통과 (96.45ms, 154MB)
테스트 2 〉	통과 (75.70ms, 126MB)
테스트 3 〉	통과 (2.94ms, 73.6MB)
테스트 4 〉	통과 (2.50ms, 90MB)
테스트 5 〉	통과 (11.34ms, 88.1MB)
테스트 6 〉	통과 (4.52ms, 84.9MB)
테스트 7 〉	통과 (5.80ms, 88.6MB)
테스트 8 〉	통과 (6.77ms, 97.4MB)
*/
class Solution {
    public int solution(int[] numbers, int target) {

        return dfs(numbers, target, 0, 0);
    }

    public int dfs(int[] numbers, int target, int sum, int idx) {
        if (numbers.length == idx) {
            return (sum == target) ? 1 : 0;
        }
        
        if (Math.abs(target-sum) > Arrays.stream(numbers).skip(idx).sum()) {
            return 0;
        } else {
            return dfs(numbers, target, sum + numbers[idx], idx+1)
                + dfs(numbers, target, sum - numbers[idx], idx+1);
        }
    }

}
```
