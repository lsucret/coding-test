
H-Index (Lv2) https://school.programmers.co.kr/learn/courses/30/lessons/42747

```java
import java.util.*;
import java.util.stream.Collectors;
class Solution {
    public int solution(int[] citations) {
        int answer = 0;
        List<Integer> citationAsc = Arrays.stream(citations) // Arrays.sort(citations) 도 가능. 단, 원본 배열이 변경됨.
            .boxed()
            .sorted(Comparator.reverseOrder())
            .collect(Collectors.toList());
        for (int i = 0; i < citationAsc.size(); i++) {
            // System.out.println( citationAsc.get(i));
            if (i + 1 <= citationAsc.get(i)) { // 3 < 
                // System.out.println( citationAsc.get(i));
                answer++;
            } else {
                break;
            }
        }
        
        return answer;
    }
}
```
