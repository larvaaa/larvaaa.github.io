

###문제
강철부대의 각 부대원이 여러 지역에 뿔뿔이 흩어져 특수 임무를 수행 중입니다. 지도에서 강철부대가 위치한 지역을 포함한 각 지역은 유일한 번호로 구분되며, 두 지역 간의 길을 통과하는 데 걸리는 시간은 모두 1로 동일합니다. 임무를 수행한 각 부대원은 지도 정보를 이용하여 최단시간에 부대로 복귀하고자 합니다. 다만 적군의 방해로 인해, 임무의 시작 때와 다르게 되돌아오는 경로가 없어져 복귀가 불가능한 부대원도 있을 수 있습니다.

강철부대가 위치한 지역을 포함한 총지역의 수 n, 두 지역을 왕복할 수 있는 길 정보를 담은 2차원 정수 배열 roads, 각 부대원이 위치한 서로 다른 지역들을 나타내는 정수 배열 sources, 강철부대의 지역 destination이 주어졌을 때, 주어진 sources의 원소 순서대로 강철부대로 복귀할 수 있는 최단시간을 담은 배열을 return하는 solution 함수를 완성해주세요. 복귀가 불가능한 경우 해당 부대원의 최단시간은 -1입니다.

###제한사항
3 ≤ n ≤ 100,000
각 지역은 정수 1부터 n까지의 번호로 구분됩니다.
2 ≤ roads의 길이 ≤ 500,000
roads의 원소의 길이 = 2
roads의 원소는 [a, b] 형태로 두 지역 a, b가 서로 왕복할 수 있음을 의미합니다.(1 ≤ a, b ≤ n, a ≠ b)
동일한 정보가 중복해서 주어지지 않습니다.
동일한 [a, b]가 중복해서 주어지지 않습니다.
[a, b]가 있다면 [b, a]는 주어지지 않습니다.
1 ≤ sources의 길이 ≤ 500
1 ≤ sources[i] ≤ n
1 ≤ destination ≤ n

### 풀이


```java
ArrayList<Integer> Answer = new ArrayList<>();
	int min;
	public int[] solution(int n, int[][] roads, int[] sources, int destination) {
        int[] answer = new int[sources.length];
        
        boolean[] visit = new boolean[n + 1];
        ArrayList<Integer>[] adjaList = new ArrayList[n + 1];
        
        //인접리스트 생성
        for(int i = 1; i <= n; i++) {
        	adjaList[i] = new ArrayList<>();
        }
        for(int i = 0; i < roads.length; i++) {
        	adjaList[roads[i][0]].add(roads[i][1]);
        	adjaList[roads[i][1]].add(roads[i][0]);
        }
        
        for(int i = 0; i < sources.length; i++) {
        	min = Integer.MAX_VALUE;
        	dfs(sources[i], destination, 0, visit, adjaList);
        	answer[i] = min;
        }
        return answer;
    }
	
	public void dfs(int start, int destination, int depth, boolean[] visit, ArrayList<Integer>[] adjaList) {
		
		if(start == destination) {
			min = Math.min(min, depth);
			return;
		}
		
		if(adjaList[start].size() == 0) {
			min = -1;
			return;
		}
		
		for(int i : adjaList[start]) {
			
			if(!visit[i]) {
				visit[i] = true;
				dfs(i, destination, depth + 1, visit, adjaList);
				visit[i] = false;
			}
		}
		
		
	}

```
