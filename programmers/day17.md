
Day 17 – 정렬 + 구현

파일명 정렬 (Lv2) https://school.programmers.co.kr/learn/courses/30/lessons/17686

```java
/*정확성  테스트
테스트 1 〉	통과 (5.63ms, 86.4MB)
테스트 2 〉	통과 (4.37ms, 94.3MB)
테스트 3 〉	통과 (29.65ms, 82.7MB)
테스트 4 〉	통과 (28.91ms, 82.7MB)
테스트 5 〉	통과 (21.38ms, 76.8MB)
테스트 6 〉	통과 (19.23ms, 81.8MB)
테스트 7 〉	통과 (19.26ms, 94.9MB)
테스트 8 〉	통과 (22.17ms, 93.2MB)
테스트 9 〉	통과 (20.31ms, 85.8MB)
테스트 10 〉	통과 (18.83ms, 98.7MB)
테스트 11 〉	통과 (21.98ms, 84.4MB)
테스트 12 〉	통과 (21.77ms, 91.4MB)
테스트 13 〉	통과 (18.59ms, 81.7MB)
테스트 14 〉	통과 (24.91ms, 79.7MB)
테스트 15 〉	통과 (35.31ms, 97.8MB)
테스트 16 〉	통과 (24.32ms, 95.2MB)
테스트 17 〉	통과 (32.50ms, 96.6MB)
테스트 18 〉	통과 (25.08ms, 94.3MB)
테스트 19 〉	통과 (18.57ms, 94.6MB)
테스트 20 〉	통과 (31.85ms, 85.7MB)
*/
import java.util.*;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

class Solution {
    public String[] solution(String[] files) {
        return Arrays.stream(files)
            .map(FileName::new)
            .sorted(new FileNameComparator())
            .map(f -> f.getFileName())
            .toArray(String[]::new);
    }
}

class FileNameComparator implements Comparator<FileName> {
    @Override
    public int compare(FileName s1, FileName s2) {
        int headResult = s1.getHead().compareToIgnoreCase(s2.getHead());
        if (headResult != 0) {
            return headResult;
        }
        return s1.getNumber() - s2.getNumber();
    }
}

class FileName {
    private String head;
    private int number;
    private String fileName;
    
    public FileName(String fileName) {
        Pattern pattern1 = Pattern.compile("\\D+"); // 숫자가 아닌 문자
        Pattern pattern2 = Pattern.compile("\\d+"); // 숫자
        Matcher matcher1 = pattern1.matcher(fileName);
        Matcher matcher2 = pattern2.matcher(fileName);
        matcher1.find();
        matcher2.find();
        this.head = matcher1.group();
        this.number = Integer.parseInt(matcher2.group(), 10);
        this.fileName = fileName;
        // System.out.println(head +","+ number);
    }
    public String getHead() {return head;}
    public int getNumber() {return number;}
    public String getFileName() {return fileName;}
}
```


```java
/*정확성  테스트
테스트 1 〉	통과 (1.09ms, 85.2MB)
테스트 2 〉	통과 (1.06ms, 78.6MB)
테스트 3 〉	통과 (4.78ms, 76.1MB)
테스트 4 〉	통과 (5.32ms, 86.1MB)
테스트 5 〉	통과 (4.61ms, 75.3MB)
테스트 6 〉	통과 (5.93ms, 81MB)
테스트 7 〉	통과 (6.13ms, 91.4MB)
테스트 8 〉	통과 (4.28ms, 83.9MB)
테스트 9 〉	통과 (4.43ms, 78.5MB)
테스트 10 〉	통과 (4.41ms, 75.4MB)
테스트 11 〉	통과 (6.59ms, 97.5MB)
테스트 12 〉	통과 (4.57ms, 82.4MB)
테스트 13 〉	통과 (3.95ms, 91.8MB)
테스트 14 〉	통과 (3.90ms, 73.7MB)
테스트 15 〉	통과 (5.70ms, 96.3MB)
테스트 16 〉	통과 (9.93ms, 80.8MB)
테스트 17 〉	통과 (4.33ms, 76.1MB)
테스트 18 〉	통과 (3.99ms, 81.8MB)
테스트 19 〉	통과 (4.33ms, 84.9MB)
테스트 20 〉	통과 (4.08ms, 84.6MB)*/
import java.util.*;

class Solution {

    private static class FilePart {
        String original;   // 원본 파일명
        String headLower;  // 비교용 head (소문자)
        int number;        // 비교용 number (정수)

        FilePart(String original, String headLower, int number) {
            this.original = original;
            this.headLower = headLower;
            this.number = number;
        }
    }

    public String[] solution(String[] files) {
        FilePart[] arr = new FilePart[files.length];

        for (int i = 0; i < files.length; i++) {
            String f = files[i];
            int n = f.length();

            // 1) HEAD 끝(= NUMBER 시작) 찾기: 첫 숫자 위치
            int idx = 0;
            while (idx < n && !Character.isDigit(f.charAt(idx))) {
                idx++;
            }
            int headEnd = idx;

            // 2) NUMBER 끝 찾기: 연속 숫자 최대 5자리
            int numStart = headEnd;
            int numEnd = numStart;
            while (numEnd < n && Character.isDigit(f.charAt(numEnd)) && (numEnd - numStart) < 5) {
                numEnd++;
            }

            String head = f.substring(0, headEnd);
            String numberStr = f.substring(numStart, numEnd);
            int number = Integer.parseInt(numberStr); // leading zero 무시됨

            arr[i] = new FilePart(f, head.toLowerCase(), number);
        }

        Arrays.sort(arr, (a, b) -> {
            int headCmp = a.headLower.compareTo(b.headLower);
            if (headCmp != 0) return headCmp;

            int numCmp = Integer.compare(a.number, b.number);
            if (numCmp != 0) return numCmp;

            // 동률이면 안정 정렬에 의해 입력 순서 유지
            return 0;
        });

        String[] answer = new String[files.length];
        for (int i = 0; i < arr.length; i++) {
            answer[i] = arr[i].original;
        }
        return answer;
    }
}

```
