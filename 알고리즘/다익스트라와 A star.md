# 다익스트라 알고리즘(Dijkstra Algorithm)과 A* 알고리즘(A star Algorithm)
## 다익스트라 알고리즘
### 개요
- 에츠허르 다익스트라가 고안한 그래프상의 최단거리 찾기 알고리즘
- 그래프의 정점의 수가 V일때, $O(V^2)$의 시간복잡도를 가진다.
- 우선순위 큐를 사용하면 그래프의 간선의 수가 E일때 $O((V+E)logV)$의 시간복잡도를 얻을 수 있다.
- 하나의 정점으로부터 다른 모든 정점들의 최단거리를 찾을 수 있다.
- 거리에 음수값이 존재할 경우, 사용할 수 없다.
- 단방향 그래프인지 양방향 그래프인지는 상관 없다.

### 과정
1. 출발점에서부터 최단거리를 저장할 배열을 d[V]를 만든다. 
2. d[V]에서 출발점에 0, 나머지는 모두 매우 큰 값을 넣는다.(예: Integer.MAX_VALUE)
3. 현재 조사중인 노드를 저장하는 변수 Node에 출발점의 인덱스를 넣는다.
4. Node에서부터 갈 수 있는 임의의 노드 A에 대해 d[Node]+Node에서 A까지의 최단거리와 d[A]를 비교한다.
5. 만약 전자의 값이 더 작다면, d[A]를 전자의 값으로 갱신한다.
6. Node에서부터 갈 수 있는 모든 노드에 대해 4~5번을 반복한다.
7. Node를 방문완료했음을 저장한다.
8. 미방문인 노드중에서 출발점에서부터 거리가 제일 짧은 노드를 골라 Node에 저장한다.
9. 구해야 하는 노드가 방문완료 상태가 되거나 더이상 미방문 상태의 노드를 선택할 수 없을때까지 4~8의 과정을 반복한다.

### Java 구현
```java
import java.util.ArrayList;
import java.util.PriorityQueue;

public class DijkstraTest {
	// 우선순위큐에 넣을 객체이므로, Comparable을 구현하거나 람다표현식을 사용해야 한다.
	private static class Vertex implements Comparable<Vertex> {
		int idx;
		int value;

		public Vertex(int idx, int value) {
			super();
			this.idx = idx;
			this.value = value;
		}

		@Override
		public int compareTo(Vertex o) {
			return this.value - o.value;
		}
	}

	public static void main(String[] args) {
		// 다익스트라에 사용할 단방향 그래프
		// 출발점을 0으로 하여 진행해보자
		ArrayList<ArrayList<Vertex>> graph = new ArrayList<>();
		for (int i = 0; i < 6; i++) {
			graph.add(new ArrayList<>());
		}

		// 그래프 입력
		graph.get(0).add(new Vertex(1, 5));
		graph.get(0).add(new Vertex(2, 2));
		graph.get(0).add(new Vertex(4, 3));
		graph.get(1).add(new Vertex(3, 3));
		graph.get(1).add(new Vertex(5, 4));
		graph.get(2).add(new Vertex(0, 4));
		graph.get(2).add(new Vertex(1, 4));
		graph.get(2).add(new Vertex(5, 7));
		graph.get(3).add(new Vertex(5, 5));
		graph.get(4).add(new Vertex(3, 2));
		graph.get(5).add(new Vertex(3, 1));

		int start = 0;
		int[] distance = new int[6];
		// 우선순위 큐의 선언과 초기화
		PriorityQueue<Vertex> q = new PriorityQueue<>();
		// 람다 표현식을 사용한 우선순위 큐의 초기화
//		PriorityQueue<Vertex> q = new PriorityQueue<>((o1, o2) -> Integer.compare(o1.value, o2.value));
		q.offer(new Vertex(start, 0));

		// distance의 초기화
		for (int i = 0; i < 6; i++) {
			distance[i] = Integer.MAX_VALUE;
		}
		distance[start] = 0;

		// Queue가 빌때까지
		while (!q.isEmpty()) {
			Vertex v = q.poll();
			System.out.println(v.idx + "에 접근중...");
			// 만약 v로 가는 값보다 기존 최단거리가 더 짧다면 중단
			if (distance[v.idx] < v.value) {
				continue;
			}
			// 현재 조사중인 정점에서 도달할 수 있는 모든 정점에 대해
			for (Vertex temp: graph.get(v.idx)) {
				// 만약 기존 최단거리보다 v를 통해 도착하는 거리가 더 짧다면 
				if (distance[temp.idx] > distance[v.idx] + temp.value) {
					// 최단거리를 업데이트 하고 우선순위 큐에 넣음
					distance[temp.idx] = distance[v.idx] + temp.value;
					q.offer(temp);
				}
			}
		}

		for (int i = 0; i < 6; i++) {
			System.out.printf("%d번째 노드까지의 최단거리: %d\n", i, distance[i]);
		}
	}
}

```

- 실행결과
```
0에 접근중...
2에 접근중...
4에 접근중...
3에 접근중...
1에 접근중...
5에 접근중...
0번째 노드까지의 최소거리: 0
1번째 노드까지의 최소거리: 5
2번째 노드까지의 최소거리: 2
3번째 노드까지의 최소거리: 5
4번째 노드까지의 최소거리: 3
5번째 노드까지의 최소거리: 9
```

### 그림으로 된 설명
![1](https://user-images.githubusercontent.com/63623597/220345655-1dfa87e6-4a6d-4e2e-a357-7120d6b8f1a0.png)<br>
![2](https://user-images.githubusercontent.com/63623597/220345663-75424b9a-39a0-490b-81b5-e3f36e6d207e.png)<br>
![3](https://user-images.githubusercontent.com/63623597/220345667-7f1be01b-e405-4247-ae43-2f3e6d5d979e.png)<br>
![4](https://user-images.githubusercontent.com/63623597/220345669-fa5c6975-dc18-421d-b809-f6e4d1901adf.png)<br>
![5](https://user-images.githubusercontent.com/63623597/220345672-3680ce95-5e63-4569-8af6-51d83b95beb9.png)<br>
![6](https://user-images.githubusercontent.com/63623597/220345673-26d8bdee-4125-4e1b-aab5-08b3400b2e08.png)<br>
![7](https://user-images.githubusercontent.com/63623597/220345676-4d6ea204-8e66-4295-ba89-bd47378799fb.png)<br>

## A* 알고리즘
### 개요
- 다익스트라 알고리즘의 확장된 알고리즘
- 출발점과 도착점이 정해져 있는 경우에 사용할 수 있다.
- 정점간의 실제 비용과 휴리스틱(heuristics)을 합쳐 다음 노드를 결정한다.
- 휴리스틱을 사용하기 때문에, 휴리스틱이 얼마나 정확한지에 따라 성능이 차이난다.

### 과정
1. 각 노드의 휴리스틱값인 h(x)와 원래 비용인 g(x)를 합쳐 f(x)를 구한다.
2. 출발점에서 도달할 수 있는 노드들을 열린 목록 O에 넣고, 출발점은 닫힌목록 C에 넣는다.
3. O에서 f(x)가 가장 낮은 노드를 고른다.
4. 다익스트라와 같은 요령으로, 아직 C에 들어있지 않으면서 최단거리 f(x)를 업데이트 할 수 있는 노드를 업데이트 하며 O에 넣는다.
5. 업데이트가 끝나면 3에서 고른 노드를 C에 넣는다.
6. 처음에 정한 도착점에 도달할때까지 3, 4, 5 과정을 반복한다.

### 그림으로 된 설명
![Astar1](https://user-images.githubusercontent.com/63623597/220345682-80e64542-2d0f-4957-8bda-e99bb76eb4da.png)<br>
![Astar2](https://user-images.githubusercontent.com/63623597/220345683-85e6caa1-f56f-47a6-a574-4da4341cee01.png)<br>
![Astar3](https://user-images.githubusercontent.com/63623597/220345687-56082ed5-8b12-42e6-9cdf-533a5a3dec5b.png)<br>
![Astar4](https://user-images.githubusercontent.com/63623597/220345690-e7f66c6f-6e6c-4e7b-90ee-64f0c1b9df18.png)<br>
![Astar5](https://user-images.githubusercontent.com/63623597/220345691-44538a9d-9524-4352-b74d-3c3ff9cb1003.png)<br>