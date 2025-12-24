
완주하지 못한 선수 (Lv1) https://school.programmers.co.kr/learn/courses/30/lessons/42576

```java
import java.util.*;

class Solution {
    public String solution(String[] participant, String[] completion) {
        Map<String, Integer> completionMap = new HashMap<>();
        for (String p : completion) {
            completionMap.merge(p, 1, Integer::sum);
        }
        for (String c : participant) {
            if (completionMap.getOrDefault(c, 0) > 0) {
                completionMap.merge(c, -1, Integer::sum);
                // System.out.println("key:"+c+", value:"+completionMap.get(c));
            } else {
                return c;
            }
        }
        return "";
    }
}
```
Big o
- 시간복잡도 : O(N)
- 공간복잡도 : O(N)
