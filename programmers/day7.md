모의고사 (Lv1) https://school.programmers.co.kr/learn/courses/30/lessons/42840

```java
// 속도 빠른 버전 (내 풀이)
import java.util.*;
class Solution {
    public int[] solution(int[] answers) {
        int[] answer = {};
        int student1 = 0;
        int student2 = 0;
        int student3 = 0;
        for (int i = 0; i < answers.length; i++) {
            if (answers[i] == answerOfStudent1(i)) {
                student1++;
            }
            if (answers[i] == answerOfStudent2(i)) {
                student2++;
            }
            if (answers[i] == answerOfStudent3(i)) {
                student3++;
            }
        }
        int max = Math.max(Math.max(student1, student2), student3);
        List<Integer> answerList = new LinkedList<Integer>();
        if (max == student1) {
            answerList.add(1);
        }
        if (max == student2) {
            answerList.add(2);
        }
        if (max == student3) {
            answerList.add(3);
        }
        return answerList.stream().mapToInt(Integer::intValue).toArray();
    }
    
    public int answerOfStudent1(int idx) {
        return idx % 5 + 1; // 0%5 + 1 = 1
        // 4: 4%5 +1 = 5
        // 5: 5%5 +1 = 1
    }
    public int answerOfStudent2(int idx) {
        int dividedEnd = idx % 8;
        switch(dividedEnd) {
            case 0: return 2;
            case 1: return 1;
            case 2: return 2;
            case 3: return 3;
            case 4: return 2;
            case 5: return 4;
            case 6: return 2;
            case 7: return 5;
            default: return 0;                
        }
    }
        public int answerOfStudent3(int idx) {
        int dividedEnd = idx % 10;
        switch(dividedEnd) {
            case 0: 
            case 1: return 3;
            case 2: 
            case 3: return 1;
            case 4: 
            case 5: return 2;
            case 6: 
            case 7: return 4;
            case 8: 
            case 9: return 5;
            default: return 0;
        }
    }

}
```

```java
// 코드 간결한 버전(ai풀이)

import java.util.*;

class Solution {
    public int[] solution(int[] answers) {
        int[] p1 = {1, 2, 3, 4, 5};
        int[] p2 = {2, 1, 2, 3, 2, 4, 2, 5};
        int[] p3 = {3, 3, 1, 1, 2, 2, 4, 4, 5, 5};

        int[] scores = new int[3];

        for (int i = 0; i < answers.length; i++) {
            if (answers[i] == p1[i % p1.length]) scores[0]++;
            if (answers[i] == p2[i % p2.length]) scores[1]++;
            if (answers[i] == p3[i % p3.length]) scores[2]++;
        }

        int max = Arrays.stream(scores).max().getAsInt();

        return java.util.stream.IntStream.range(0, 3)
                .filter(i -> scores[i] == max)
                .map(i -> i + 1)
                .toArray();
    }
}

```
