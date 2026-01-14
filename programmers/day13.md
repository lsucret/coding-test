
Day 13 – 문자열 / 구현

문자열 압축 (Lv2) https://school.programmers.co.kr/learn/courses/30/lessons/60057

StringBuilder idea 도출은 금방이었으나, 디버깅에 시간이 걸렸다.
```java
import java.util.*;

class Solution {
    public int solution(String s) {
        int maxSlice = s.length() / 2;
        int answer = s.length();
        
        for (int j = 1; j <= maxSlice; j++) {
        
            StringBuilder sb = new StringBuilder();
            int count = 1;
            String cursor = "";
            for (int i = 0; i < s.length(); i += j) {
                String pointer = s.substring(i, Math.min(i + j, s.length()));
                // if (j == 1) System.out.println("i:"+i+",pointer:"+pointer+",count:"+count + ",sb:"+sb.toString());
                
                if (cursor.equals(pointer)) {
                    ++count;
                    // System.out.println(s.length() <= Math.min(i + j, s.length()));
                } else {
                    if (j == 1) System.out.println(((count == 1) ? "" : count) + cursor);
                    sb.append(((count == 1) ? "" : count) + cursor);
                    count = 1;
                    cursor = pointer;
                }
                    if (s.length() <= Math.min(i + j, s.length())) {
                        sb.append(((count == 1) ? "" : count) + cursor);
                    }
            }
            String ss = sb.toString();
            answer = Math.min(answer, ss.length());
        }
        
        return answer;        
    }
}
// 
```
