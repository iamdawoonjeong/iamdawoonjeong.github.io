---
layout: single
title: "[Problem Solving - Baekjoon] 1939 중량제한"
date: 2020-11-02 23:36:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Problem Solving
tags:
- data structure
- algorithm
- BFS
- binary search
- baekjoon
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-1939/"
---
# [Baekjoon Online Judge] 1939 중량제한

## 문제
N(2≤N≤10,000)개의 섬으로 이루어진 나라가 있다. 이들 중 몇 개의 섬 사이에는 다리가 설치되어 있어서 차들이 다닐 수 있다.

영식 중공업에서는 두 개의 섬에 공장을 세워 두고 물품을 생산하는 일을 하고 있다. 물품을 생산하다 보면 공장에서 다른 공장으로 생산 중이던 물품을 수송해야 할 일이 생기곤 한다. 그런데 각각의 다리마다 중량제한이 있기 때문에 무턱대고 물품을 옮길 순 없다. 만약 중량제한을 초과하는 양의 물품이 다리를 지나게 되면 다리가 무너지게 된다.

**한 번의 이동에서 옮길 수 있는 물품들의 중량의 최댓값**을 구하는 프로그램을 작성하시오.

### 입력
첫째 줄에 N, M(1≤M≤100,000)이 주어진다. 다음 M개의 줄에는 다리에 대한 정보를 나타내는 세 정수 A, B(1≤A, B≤N), C(1≤C≤1,000,000,000)가 주어진다. 이는 A번 섬과 B번 섬 사이에 중량제한이 C인 다리가 존재한다는 의미이다. 서로 같은 두 도시 사이에 여러 개의 다리가 있을 수도 있으며, 모든 다리는 양방향이다. 마지막 줄에는 공장이 위치해 있는 섬의 번호를 나타내는 서로 다른 두 정수가 주어진다. 공장이 있는 두 섬을 연결하는 경로는 항상 존재하는 데이터만 입력으로 주어진다.

### 출력
첫째 줄에 답을 출력한다.

### 예제
- input

```java
3 3
1 2 2
3 1 3
2 3 2
1 3
```

- output

```java
3
```

### 분류
- 이진탐색
- BFS

## 풀이

### 문제 파악

- 공장이 세워진 1번에서 3번섬까지 물품들의 중량의 최댓값 찾기

```java
3 3  // 섬의갯수 :n , 다리의 갯수 m
1 2 2 // 1번섬과 2번섬의 무게제한은 2
3 1 3
2 3 2
1 3    // 공장위치한 섬의번호 1, 3
```

- 양방향 가중치 트리
- 가장 가까운 노드를 선택하고 탐색되지 않은 모든 노드를 탐색하는 [BFS(Breath First Search)](http://dawoonjeong.com/algorithm-graph-bfs-dfs/)으로 풀어야할 문제  
- [공유기설치](http://dawoonjeong.com/algorithm-problem-solving-baekjoon-2110/) 문제처럼 [binary search](http://dawoonjeong.com/algorithm-search/)로 최대 중량을 찾아야 함


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1939/Main.java)

- graph의 vertex(node)를 class로 생성

```java
private static ArrayList<Vertex>[] graph ;

class Vertex{
    int end;
    int wieght;

    Vertex(int end, int weight) {
        this.end = end;
        this.wieght = weight;
    }
}
```

- 입력된 섬의 갯수(n)만큼 정점을 만듦

```java
graph = new ArrayList[n+1];

for (int i = 0; i <= n; i++) {
    //adjacent
    graph[i] = new ArrayList<Vertex>();
}
```

- 문제에서 가질 수 있는 최소중량 1과 문제에서 가질 수 있는 최대중량 1,000,000,000 을 선언
- 나중에 math함수 이용해 입력된 값과 비교

```java
int maxWeight = 1;         
int minWeight = 100000000;
```


- 입력된 다리의 갯수(m)만큼 edge 연결

```java
for (int i = 0; i < m; i++) {

	st = new StringTokenizer(br.readLine());

	int from = Integer.parseInt(st.nextToken());
	int to = Integer.parseInt(st.nextToken());
	int weight = Integer.parseInt(st.nextToken());

	//from 에서 to 까지의 중량제한 weight이며, 양방향임
	graph[from].add(new Vertex(to, weight));
	graph[to].add(new Vertex(from, weight));

	//주어진 예에서 섬 사이의 최대/최소 제한중량찾기
	maxWeight= Math.max(maxWeight, weight);
	minWeight= Math.min(minWeight, weight);
}
```

- binarySearch 기법으로 mid을 찾은 다음에 다리를 통과하면 mid +1 해서 다시 시도, 통과하지 못하면 mid-1로 시도

```java
static void binarySearch(int n, int startNode, int endNode, int maxWeight, int minWeight) {

    int low = minWeight;
    int high = maxWeight;

    //binary search로 최대중량 찾기
    while(low <= high) {
        int mid = (low + high)/2; //현재 중량 mid = 2;

        //현재 중량으로 이동가능여부 판단
        if (bfs(n,  mid, startNode, endNode)) {
            //이동 가능하므로 중량 늘리기
            result = Math.max(result, mid);
            low = mid +1;
        }else {
            //이동 불가하므로 중량 줄이기
            high = mid-1;
        }
    }
}
```

- binarySearch 로 찾은 mid 값으로 bfs 기법으로 다리를 통과해보기

```java
static boolean bfs(int n, int mid, int startNode, int endNode) {
    Queue<Integer> queue = new LinkedList<Integer>();
    boolean visited[] = new boolean[n+1]; //방문여부

    queue.add(startNode);       //출발 공장 추가
    visited[startNode] = true;  //출발 공장은 방문함

    // queue가 empty가 아닐때까지 head를 poll 하여 출력
    while(!queue.isEmpty()) {
        //queue의 head를 출력
        int head = queue.poll();

        //head 부터 트리 순회
        for (Vertex v : graph[head]) {
            //정점의 중량이 현재중량 보다 클 경우 통과 가능
            if (v.wieght >= mid) {
                //poll한 노드가 도착공장인 경우 방문 완료 했음으로 리턴
                if (head == endNode) {
                    return true;
                }

                if(!visited[v.end]) {
                    //방문여부 체크후 queue에 add
                    visited[v.end] = true;
                    queue.add(v.end);
                }
            }
        }
    }
    return visited[endNode];
}   
```

---

#### references
<https://www.acmicpc.net/problem/1939>
