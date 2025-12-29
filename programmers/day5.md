https://school.programmers.co.kr/learn/courses/30/lessons/42586

```java
import java.util.*;

class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
        int days = 0;
        List<Integer> deployCount = new ArrayList(); // arrayList 대신 LinkedList를 사용하면 addLast 같은걸 써서 코드 간결.
        // LinkedList<Integer> deployCount = new LinkedList<>();
        for (int i = 0; i < progresses.length; i++) {
            int workingDay = divideFloor(100 - progresses[i], speeds[i]);
            if (days < workingDay) {
                days = workingDay;
                deployCount.add(1);
            } else {
                int lastIndex = deployCount.size() - 1;
                deployCount.set(lastIndex, deployCount.get(lastIndex) + 1);
            }
        }
        
        return deployCount.stream().mapToInt(Integer::intValue).toArray();
    }
    
    public int divideFloor(int a, int b) {
        return (a / b) + ((a % b == 0) ? 0 : 1);
    }
}
```

