---
title: 프로그래머스 lv2 무인도 여행
---

```java
String[][] Maps;
boolean[][] Visit;
List<Integer> Answer;
int sum;

public int[] solution(String[] maps) {

  int[] answer = {};

      Answer = new ArrayList<>();
      int n = maps.length;
      int m = maps[0].split("").length;

      Visit = new boolean[n][m];
      Maps = new String[n][m];

      for(int i = 0; i < n; i++) {
        for(int j = 0; j < m ; j++) {
          Maps[i][j] = String.valueOf(maps[i].charAt(j));
        }
      }

      for(int i = 0; i < n; i++) {
        for(int j = 0; j < m; j++) {
          if(!Visit[i][j] && !Maps[i][j].equals("X")) {
            sum = Integer.parseInt(Maps[i][j]);
            dfs(i, j, n, m);
            Answer.add(sum);
          }
        }
      }
      if(Answer.size() == 0) answer = new int[] {-1};
      else answer = new int[Answer.size()];

      for(int i = 0; i < Answer.size(); i++) {
        answer[i] = Answer.get(i);
      }
      Arrays.sort(answer);
      return answer;
  }


void dfs(int x, int y, int n, int m) {

  Visit[x][y] = true;

  int[] dx = {0, 1, -1, 0};
  int[] dy = {1, 0, 0, -1};

  for(int i = 0; i < 4; i++) {

    int nx = x + dx[i];
    int ny = y + dy[i];

    if(nx < 0 || ny < 0 || nx >= n || ny >= m) continue;

    if(!Visit[nx][ny] && !Maps[nx][ny].equals("X")) {
      sum+=Integer.parseInt(Maps[nx][ny]);
      dfs(nx, ny, n, m);
    }

  }

}
```
