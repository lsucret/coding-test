Day 11 – 해시 응용

의상 (Lv2) https://school.programmers.co.kr/learn/courses/30/lessons/42578


```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int solution(String[][] clothes) {
        // 의상 종류별 개수를 저장할 HashMap
        Map<String, Integer> clothesMap = new HashMap<>();
        
        // 각 의상을 종류별로 분류하여 개수 세기
        for (String[] cloth : clothes) {
            String type = cloth[1];  // 의상 종류
            clothesMap.put(type, clothesMap.getOrDefault(type, 0) + 1);
        }
        
        // 각 종류별로 (개수 + 1) 을 곱함
        // +1은 그 종류의 의상을 입지 않는 경우
        int answer = 1;
        for (int count : clothesMap.values()) {
            answer *= (count + 1);
        }
        
        // 전부 입지 않는 경우 1을 빼기
        return answer - 1;
    }
}
```
