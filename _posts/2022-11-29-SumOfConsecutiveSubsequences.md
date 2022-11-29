---
title: 프로그래머스 lv2 연속 부분 수열 합의 개수
---

원형(연속하는 배열)이라서 인덱스의 반복이 필요하다.   
arr[idx % arr.length]   

>개수가 1일때 합   
>개수가 2일때 합   
>      .   
>      .   
>      .   
>개수가 n일대 합   
이런식으로 각가의 합을 구해서 set에 추가한다.



```java
public int solution(int[] elements) {
    int answer = 0;

    Set<Integer> sums = new HashSet<>();
    for(int i = 1; i <= elements.length; i++) {//1개 합, 2개합 .. n개합

      for(int j = 0; j < elements.length; j++) {  
        int sum = 0;
        for(int k = j; k < j + i; k++) {
          sum += elements[k % elements.length];
        }
        sums.add(sum);
      }

    }

    answer = sums.size();
    return answer;
}
```
