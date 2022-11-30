---
title: 프로그래머스 lv3 억억단을 외우자
---


문제: 임의의 수 e,  e 이하의 임의의 수 s가 배열로 주어진다.   
s보다 크거나 같고 e 보다 작거나 같은 수 중에서 억억단에서 가장 많이 등장한 수를 구한다.   
만약 가장 많이 등장한 수가 여러 개라면 그 중 가장 작은 수를 답해야 한다.   
   
__제한사항__   
  *1 ≤ e ≤ 5,000,000   
  *1 ≤ starts의 길이 ≤ min {e,100,000}   
  *1 ≤ starts의 원소 ≤ e   
  *starts에는 중복되는 원소가 존재하지 않습니다.   
   




```java
public int[] solution(int e, int[] starts) {
    int[] answer = new int[starts.length];

    HashMap<Integer,Integer> map = new HashMap<>();

    //결과값 개수 구하기
    for(int j = 1; j <= e; j++) {
      for(int k = 1; k <= j; k++) {
        if(j * k > e) break;
        else if(j == k) map.put((j * k), map.getOrDefault((j * k), 0) + 1);
        else if(j != k) map.put((j * k), map.getOrDefault((j * k), 0) + 2);
      }
    }

    List<int[]> list = new ArrayList<>();
    for(Entry<Integer, Integer> entry : map.entrySet()) list.add(new int[] {entry.getKey(), entry.getValue()});
    Collections.sort(list, new Comparator<int[]>() {
      @Override
      public int compare(int[] o1, int[] o2) {
        if(o1[1] == o2[1]) return o1[0] - o2[0];
            return o2[1] - o1[1];
      }
});

    for(int i = 0; i < starts.length; i++) {

      int idx = 0;
      for(int j = 0; j < list.size(); j++) {
        if(list.get(j)[0] <= e && list.get(j)[0] >= starts[i]) {
          idx = list.get(j)[0];
          break;
        }
      }
      answer[i] = idx;
    }


    return answer;
}
```
