
Day 18 – 이분 탐색

입국심사 (Lv3) https://school.programmers.co.kr/learn/courses/30/lessons/43238

우선순위큐로 하다 실패.

이분 탐색만이 시공간복잡도를 줄여줌

시간복잡도

`O( m⋅log(n⋅max(times)) )`
- m: 심사관 수 (최대 10만)
- n: 사람 수 (최대 1억)
- max(times): 가장 느린 심사관의 처리 시간

```java
import java.util.*;

class Solution {
    public long solution(int n, int[] times) {
        long lo = 0L;
        long max = 0L;
        for (int t : times) {
            if (t > max) max = t;
        }
        long hi = max * (long) n;  // 가능한 최대 시간(상한)

        while (lo < hi) {
            long mid = lo + (hi - lo) / 2;

            long processed = 0L;
            for (int t : times) {
                processed += mid / t;
                // n 이상이면 더 셀 필요 없음(오버플로/시간 절약)
                if (processed >= n) break;
            }

            if (processed >= n) {
                hi = mid;      // mid 시간으로 가능 → 더 줄여본다
            } else {
                lo = mid + 1;  // mid 시간으로 불가 → 늘린다
            }
        }
        return lo;
    }
}

```
