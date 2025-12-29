// https://school.programmers.co.kr/learn/courses/30/lessons/12909
속도는 1번이 빠르나 스택 연습용으로 2번 방식도 풀이.

```java
class Solution {
    boolean solution(String s) {
        int num = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                num += 1;
            } else {
                num -= 1;
            }
            if (num < 0) {
                return false;
            }
        }

        return num == 0;
    }
}
```

```java
import java.util.*;

class Solution {
    boolean solution(String s) {
        Stack<Character> str = new Stack();
        
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == '(') {
                str.push(c);
            } else if (c == ')' && str.empty()) {
                return false;
            } else {
                str.pop();
            }
        }
        return str.empty();
    }
}
```


