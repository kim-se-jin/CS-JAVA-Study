# 그래프
 그래프는 노드(N,node)와 그 노드를 연결하는 간선(E,dege)으로 이루어진 자료구조로, 연결되어 있는 객체 간의 관계를 표현할 수 있는 자료구조 입니다. 예를 들어 지도, 지하철 노선도, 도로(교차선, 일방통행길) 등 이 있습니다.

### Q) 그래프 탐색 기법인 BFS, DFS 에 대해 설명해주세요. 
(V : vertex 정점, E : edge 간선 )   
**깊이 우선 탐색 (DFS)**   
- 시작정점에서 시작하여 다음 분기로 넘어가기 이전 해당 분기를 완벽하게 탐색, 즉 **깊이를 우선적으로 탐색하는 방식**을 말합니다. 
- **재귀나 스택**을 사용하여 구현할 수 있으며, **인접리스트로 구현시* O(V*E)***, 인접행렬로 구현 시 O(V^2) 시간복잡도가 소요됩니다.

<img src="https://user-images.githubusercontent.com/67494004/231199809-65a48f05-fe51-4294-9ccf-54525a2ae0c7.png" width="640" height="500">



<details>
<summary>재귀를 사용한 DFS JAVA 코드</summary>
  
  
  
```java
  static ArrayList<ArrayList<Integer>> graph; // 그래프
  static boolean[] visited; // 방문 여부를 저장하는 배열

  static void dfs(int node) {
      visited[node] = true; // 현재 노드를 방문 처리
      System.out.print(node + " "); // 현재 노드 출력

      // 현재 노드와 연결된 인접 노드들을 재귀적으로 방문
      for (int i : graph.get(node)) {
          if (!visited[i]) {
              dfs(i);
          }
      }
  }
```
  
  
  
</details>


**너비 우선 탐색 (BFS)**

- 시작 정점에서 시작하여 인접한 노드를 먼저 탐색, 즉 **너비를 우선적으로 탐색하는 방식**을 말합니다. 
- **큐**를 사용하여 구현할 수 있으며, **인접리스트로 구현 시  O(V*E)**, 인접행렬로 구현 시 O(V^2) 시간복잡도가 소요됩니다.
<img src="https://user-images.githubusercontent.com/67494004/231199831-003ed0ec-eb05-424b-8bad-40eb385dec0d.png" width="600" height="680">


<details>
<summary>BFS JAVA 코드</summary>
  
  
  
```java
  static void bfs(int start) {
      Queue<Integer> queue = new LinkedList<>();
      visited[start] = true; // 시작 노드를 방문 처리
      queue.offer(start); // 시작 노드를 큐에 추가

      while (!queue.isEmpty()) {
          int node = queue.poll(); // 큐에서 노드를 꺼내옴
          System.out.print(node + " "); // 현재 노드 출력

          // 현재 노드와 연결된 인접 노드들을 큐에 추가하고 방문 처리
          for (int i : graph.get(node)) {
              if (!visited[i]) {
                  visited[i] = true;
                  queue.offer(i);
              }
          }
      }
  }
```
  
  
  
</details>

  
  ### Q-1) 각각 상황의 예시를 들어주세요.
  - DFS : 검색 대상 그래프가 많이 클 때
  - BFS:  미로찾기 등 최단 거리를 구해야 할 때

### Q) 최소 신장 트리가 무엇인 지, 최소 신장 트리 알고리즘 기법 중 하나에 대해 설명해주세요.
최소 신장 트리는 Spanning Tree 중에서 사용된 간선들의 가중치 합이 최소인 트리입니다. 조건으로는 `간선의 가중치의 합이 최소`, `n개의 정점을 가지는 그래프에 대해 반드시 (n-1)개의 간선만을 사용`, `사이클이 포함되어서는 안됨` 이 있습니다.

알고리즘 기법으로는, **Kruscal 알고리즘**과 Prim 알고리즘 기법이 있습니다. 
크루스칼 알고리즘에 대해 설명해보자면, 모든 노드를 연결하면서 가중치의 합이 최소가 되는 최소 신장 트리를 찾는 알고리즘입니다.
```
1. 간선 비용 순으로 오름차순 정렬
2. 낮은 비용부터 연결된 정점들을 유니온 파인드 기법으로 연결
3. 거리를 더해줌
4. 최종적으로 하나의 연결된 선분 형성
```



방식으로 모든 정점의 최소 비용을 구합니다.
- 시간복잡도는 간선의 개수를 E, 노드의 개수를 V라고 할 때, 간선의 **정렬**에 `O(E log E)`의 시간이 소요되며, 그 외에 **유니온-파인드(Union-Find) 자료구조를 사용**하여 사이클 검사에 `O(log V)`의 시간이 소요됩니다. 따라서 **크루스칼 알고리즘의 총 시간복잡도는 `O(E log E + E log V)`** 입니다. 

<details>
<summary>Kruscal JAVA 코드</summary>
  
  
  
 ```java
 // 크루스칼 알고리즘
    public void kruskalMST() {
        // 간선을 가중치를 기준으로 정렬
        ArrayList<Edge> edges = new ArrayList<>();
        for (int i = 0; i < V; i++) {
            for (Edge edge : adjList[i]) {
                edges.add(edge);
            }
        }
        Collections.sort(edges); // 가중치를 기준으로 정렬

        int[] parent = new int[V]; // 부모 노드 배열
        for (int i = 0; i < V; i++) {
            parent[i] = i; // 처음에는 모든 노드의 부모를 자기 자신으로 초기화
        }

        ArrayList<Edge> mst = new ArrayList<>(); // 최소 신장 트리를 구성하는 간선들의 리스트

        for (Edge edge : edges) {
            int srcRoot = find(parent, edge.src); // 시작점의 루트 노드
            int destRoot = find(parent, edge.dest); // 도착점의 루트 노드

            if (srcRoot != destRoot) { // 사이클을 형성하지 않는 경우에만 선택
                mst.add(edge); // 간선을 최소 신장 트리에 추가
                union(parent, srcRoot, destRoot); // 두 노드의 루트를 합침
            }

            if (mst.size() == V - 1) { // 모든 노드를 연결한 경우 종료
                break;
            }
        }

        // 최소 신장 트리 출력
        System.out.println("최소 신장 트리 간선들:");
        for (Edge edge : mst) {
            System.out.println(edge.src + " - " + edge.dest + " : " + edge.weight);
        }
    }

    // 노드의 루트 노드를 찾는 함수
    private int find(int[] parent, int node) {
      if (parent[node] != node) {
        parent[node] = find(parent, parent[node]); // 경로 압축 최적화
      }
      return parent[node];
    }
  
  // 두 노드를 합치는 함수
  private void union(int[] parent, int x, int y) {
      int rootX = find(parent, x);
      int rootY = find(parent, y);
      parent[rootX] = rootY;
  }
```
  
  
  
</details>
 

### Q) 그래프를 표현하는 방식에서 인접 행렬과 인접 리스트가 있었습니다. 단거리 알고리즘 중 무조건 인접 행렬을 사용해야 하는 알고리즘은 뭘까요?
- 모든 정점 사이의 최단 거리를 구하는 **플로이드-워셜 알고리즘**에서는 인접행렬을 사용해야 합니다.
  
  
<details>
<summary> Floyd-Warshall JAVA 코드</summary>
  
  
  
```java
public class Main {
 
    static int INF = 10000001;

    public static void main(String args[])  {
        // 결과를 저장할 2차원 배열 초기화
        int[][] dists = new int[N][N];

        for(int i=0;i<N;i++) Arrays.fill(dists[i],INF);
        
        for(int i=0;i<M;i++){
            int x = x값;
            int y = y값;
            int cost = 비용;
            dists[x][y] = Math.min(cost, dists[x][y]);
        }
        
        floyd();
    }

    public static void floyd(){
	// 중간 노드를 거쳐가는 모든 경로에 대한 최단 경로를 찾음
        for(int k=0;k<N;k++){ 
            for(int i=0;i<N;i++){
                for(int j=0;j<N;j++){
                    if(i==j) dists[i][j] = 0 ;
                    dists[i][j] = Math.min(dists[i][k]+dists[k][j], dists[i][j]);
                }
            }
        }
    }
}
```
  
  
  
</details>
  
  

  ### Q-1) 그와 연관된 다익스트라 알고리즘의 시간 복잡도에 대해 설명해주세요.
  우선순위큐 + 인접 리스트 O(E*logV), 인접 행렬 O(V^2) 입니다.
  
  
  <details>
<summary> Dijkstra JAVA 코드</summary>
  
  
  
```java
import java.util.*;

public class Main {
    private static final int INF = 999999; // 무한대 값으로 초기화

    static class Node implements Comparable<Node> {
        int vertex;
        int weight;

        public Node(int vertex, int weight) {
            this.vertex = vertex;
            this.weight = weight;
        }

        @Override
        public int compareTo(Node o) {
            return this.weight - o.weight;
        }
    }

    public static void dijkstra(List<List<Node>> graph, int start, int V) {
        int[] dist = new int[V];
        Arrays.fill(dist, INF); // 초기 거리 값을 무한대로 설정
        dist[start] = 0; // 시작 노드의 거리는 0으로 설정

        PriorityQueue<Node> pq = new PriorityQueue<>();
        pq.offer(new Node(start, 0)); // 시작 노드를 우선순위 큐에 넣음

        while (!pq.isEmpty()) {
            Node curNode = pq.poll(); // 우선순위 큐에서 가장 작은 거리를 가진 노드를 꺼냄
            int curVertex = curNode.vertex;
            int curWeight = curNode.weight;

            if (curWeight > dist[curVertex]) continue; // 현재 거리가 기존에 계산된 거리보다 크다면 무시

            for (Node nextNode : graph.get(curVertex)) {
                int nextVertex = nextNode.vertex;
                int nextWeight = nextNode.weight;

                // 다음 노드까지의 거리가 더 작으면 업데이트하고 우선순위 큐에 넣음
                if (dist[nextVertex] > dist[curVertex] + nextWeight) {
                    dist[nextVertex] = dist[curVertex] + nextWeight;
                    pq.offer(new Node(nextVertex, dist[nextVertex]));
                }
            }
        }

        // 결과 출력
        System.out.println("시작 노드로부터의 최단 경로:");
        for (int i = 0; i < V; i++) {
            System.out.println("노드 " + i + ": " + dist[i]);
        }
    }
```
  
  
  
</details>


  ### Q-2) 다익스트라 알고리즘은 `O(E*logV)`, 플로이드 워셜 알고리즘은 `O(V^3)` 의 시간복잡도가 소요됩니다. 이 때, 다익스트라로 모든 정점을 구한다면 `O(V*E*logV)`인데 그럼 다익스트라가 빠를까요, 플로이드 워셜이 빠를까요?
  **플로이드 워셜**이 더 빠릅니다. 
    
  ### Q-2-1) 왜 그럴까요?
  [실제 문제](https://www.acmicpc.net/problem/21940)를 풀던 중, 플로이드 워셜이 다익스트라보다 더 빠른 시간복잡도를 가짐을 발견했습니다.
    
  - 플로이드 워셜 알고리즘은 정점 개수에 상관없이 한 번의 실행으로 모든 정점 쌍에 대한 최단 경로를 구할 수 있습니다. 
    - 따라서 정점 개수가 적을 때에도 동적 프로그래밍 방식으로 한 번에 최단 경로를 구하므로 **시간복잡도가 `O(V^3)`으로 고정**됩니다. 
    - 반면에 **다익스트라 알고리즘**은 시작 노드로부터 각 정점까지의 최단 경로를 그리디하게 선택하면서 구하므로, 정점 개수만큼 반복하면서 각 정점을 방문해야 하기 때문에 **시간복잡도가 `O(V*ElogV)`가** 될 수 있습니다.
    
 <img width="819" alt="image" src="https://user-images.githubusercontent.com/67494004/231215019-dff87d5d-92b5-4e06-ba0e-013e9d8bc77d.png">
    
    
    
  - **정점의 개수가 같고, 간선의 개수가 달라질 때** 
    - 플로이드 워셜은 동일한 시간복잡도를 유지
    - 다익스트라는 급격히 늘어남
  - 따라 **정점의 개수가 적을 때에는 플로이드 워셜을 사용**하는 게 오히려 다익스트라를 정점 개수만큼 반복했을 때 보다 **빠릅니다.**   

  ### Q-3) 다익스트라 알고리즘의 단점에 대해 알려주세요.
  음의 간선이 있을 때 사용할 수 없습니다.

  ### Q-4) 그럴 때 벨만포드 알고리즘을 사용하는데, 벨만포드만의 단점은 뭘까요?
  매번 모든 간선을 확인하기 때문에 다익스트라보다 시간복잡도`O(V*E)`가 오래 소요된다는 단점이 있습니다.
  
  ### Q-5) 음수의 가중치가 존재한다고 했을 때, 벨만포드로 무조건 최단거리를 구할 수 있을까요?
  > 💡! 없는 경우가 있습니다.
  - 음수 가중치 사이클에 대한 처리가 필요합니다.음수의 가중치가 양수의 가중치보다 넓을 때 순환을 이루게 될 때, 계속 음수값이 업데이트가 되므로 결국 모든 최단거리가 -무한대가 됩니다. 이럴 경우, 계속 업데이트됨을 알려 최단 경로가 될 수 없다를 명시해줘야 합니다.
    
  <details>
<summary> BellmanFord JAVA 코드</summary>
  
  
  
```java
    void BellmanFord(Graph graph, int src) {
        int V = graph.V;
        int E = graph.E;
        int[] dist = new int[V];

        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[src] = 0;

        for (int i = 1; i < V; ++i) {
            for (int j = 0; j < E; ++j) {
                int u = graph.edges[j].src;
                int v = graph.edges[j].dest;
                int weight = graph.edges[j].weight;
                if (dist[u] != Integer.MAX_VALUE && dist[u] + weight < dist[v])
                    dist[v] = dist[u] + weight;
            }
        }

        for (int j = 0; j < E; ++j) {
            int u = graph.edges[j].src;
            int v = graph.edges[j].dest;
            int weight = graph.edges[j].weight;
            if (dist[u] != Integer.MAX_VALUE && dist[u] + weight < dist[v]) {
                System.out.println("음수 사이클이 존재합니다.");
                return;
            }
        }

        printSolution(dist, V);
    }
```
  
  
  
</details>
    

