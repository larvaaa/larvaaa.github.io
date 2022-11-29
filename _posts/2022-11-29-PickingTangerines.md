---
title: 프로그래머스 lv2 귤 고르기
---

```java
public int solution(int k, int[] tangerine) {
    int answer = 0;

    int[] size = new int[10000001];
    for(int i : tangerine) size[i]++;
    int cnt = tangerine.length;

    Arrays.sort(size);
    a : for(int i = 1; i < size.length; i++) {
      cnt -= size[i];
      if(cnt < k) {
        for(int j = i; j < size.length; j++) {
          if(size[j] > 0) answer++;
        }
        break a;
      }
    }

    return answer;
}
```
