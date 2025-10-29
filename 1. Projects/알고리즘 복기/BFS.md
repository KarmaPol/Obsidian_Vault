```java
import java.util.*;

class Solution {
    private boolean[] visited = new boolean[205];
    
    public int solution(int n, int[][] computers) {
        int answer = 0;
        Queue<Integer> q = new LinkedList<>();
        
        // 1. 첫 시작 지점 순회
        for(int i = 0; i < n; i++) {
            if(!visited[i]) {
                answer++;
                q.add(i);
                visited[i] = true;
                bfs(q, computers);
            }
        }
                
        return answer;
    }
    
    private void bfs(Queue<Integer> q, int[][] computers) {
        while(!q.isEmpty()) {
            Integer node = q.peek();
            q.poll();
            
            for(int j = 0; j < computers[node].length; j++) {
                if(!visited[j] && computers[node][j] == 1) {
                    visited[j] = true;
                    q.add(j);
                }
            }
        }
    }
}
```