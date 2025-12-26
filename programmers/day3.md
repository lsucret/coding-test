https://school.programmers.co.kr/learn/courses/30/lessons/42577

전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.

- 시간 복잡도: O(nlogn)
- 공간 복잡도: O(n)
```java
import java.util.*;
class Solution {
    public boolean solution(String[] phone_book) {
        boolean answer = true;
        // String[] a = {"02","10", "1", "111", "2", "229", "23", "231"}; // 02, 1, 10, 111, 2, 229, 23, 231
        // Arrays.sort(a);
        // System.out.println(a[0]+","+a[1]+","+a[2]+","+a[3]+","+a[4]+","+a[5]+","+a[6]);
        
        Arrays.sort(phone_book);
        int length = phone_book.length;
        for (int i = 0; i < length; i++) {
            if (i + 1 >= length) {
                break;
            } else if (phone_book[i].startsWith(phone_book[i+1])
                      || phone_book[i+1].startsWith(phone_book[i])) {
                answer = false;
                break;
            }
        }
        
        return answer;
    }
}
```
