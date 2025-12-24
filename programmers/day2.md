

K번째수 (Lv1) https://school.programmers.co.kr/learn/courses/30/lessons/42748

```java
import java.util.*;
import java.util.stream.IntStream;

class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];
        int idx = 0;
        
        for (int[] command : commands) {
            int i = command[0], j = command[1], k = command[2];
            answer[idx] = IntStream.rangeClosed(command[0] - 1, command[1] - 1)
                .map(pos -> array[pos])
                .sorted()
                .skip(k-1)
                .findFirst()
                .getAsInt();
            idx++;
        }
        return answer;
    }
}
```

> note : 배열은 무조건 값을 넣기전에 길이가 결정되어야 한다.
> int[] answer = {}; 는 안됨. (문제 템플릿 코드가 저렇게 나옴)


