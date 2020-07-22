---
layout: single
title: "[Data Structure] 비선형 자료구조(2)  - 그래프(Graph)"
date: 2020-07-14 21:54:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- DataStructure
tags:
- data structure
- algorithm
- graph
- BFS
- DFS
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/datastructure-non-linear-data-structure-graph/"
---
# [Data Structure] 비선형 자료구조(2)  - 그래프(Graph)
- 트리(Tree)
- **그래프(Graph)**


## 그래프 Graph
- vertex와 edge연결선의 집합으로 정의
- vertex or node (정점) : 그래프의 각 노드는 정점으로 표시   V = {0,1,2,3,4}
- edge or arc (연결선) : 두 정점 사이의 경로 또는 두 정점 사이의 선  E = {01, 12, 23, 34, 04, 14, 13}
- adjacent (인접성) : 두 노드 또는 꼭지점이 가장자리를 통해 서로 연결된 경우 인접이라고 함. 2는 1에 인접하고, 1은 0에 인접함
- path (경로) : 두 정점 사이의 일련의 가장자리. 210은 2에서0의 경로를 나타냄
- Closed Path (닫힌 경로) : 초기 노드가 터미널 노드와 동일한 경우. V<sub>0</sub>=V<sub>N</sub>인 경우의 경로
- Simple Path (간단한 경로) : 그래프의 모든 노드가 예외 V<sub>0</sub>=V<sub>N</sub>으로 구별되는 경우의 경로
- Cycle (주기) : 사이클은 첫 번째 정점과 마지막 정점을 제외하고 반복 된 모서리나 정점이 없는 경로
- Loop (고리) : 유사한 종점과 관련된 모서리를 루프라고
- Degree of the Node (노드의 정도) :  해당 노드와 연결된 edgt 수. 차수가 0 인 노드는 격리 된 노드라고 함

#### undirected graph, graph (무방향성그래프)
- n개의 정점으로 구성되는 무방향성그래프에서 complete graph가 가질수 있는 연결선의 최대수는 n(n-1)/2
![datastructure-undirectedgraph]({{ site.baseurl }}/assets/images/posts/2020/datastructure-undirectedgraph.png)


#### directed graph, digraph (방향성그래프)
- 각 가장자리가 특정 방향과 연관되어 있고 지정된 방향으로만 이송 할 수있는 유방향 그래프
- n개의 정점으로 구성되는 방향성 그래프에서 complete graph가 가질 수 있는 연결선의 최대수는 n-1
![datastructure-directed-graph]({{ site.baseurl }}/assets/images/posts/2020/datastructure-directed-graph.png)


#### Complete Graph (완전한 그래프)  
- 모든 노드가 다른 모든 노드와 연결된 그래프. 노드의 수가 n개일 경우, 연결선의 최대수는 n (n-1) / 2
![datastructure-complete-graph]({{ site.baseurl }}/assets/images/posts/2020/datastructure-complete-graph.png)


#### Weighted Graph (가중 그래프)
- 각 모서리에는 길이 또는 무게와 같은 일부 데이터가 할당됨.  
- edge의 E의 가중치는 w(E)로 주어질 수 있으며, 이는 edge를 순회하는 비용을 나타내는 양수 (+) 값 이여야 함
- Sequential Representation


![datasturcture-sequential-representation3]({{ site.baseurl }}/assets/images/posts/2020/datasturcture-sequential-representation3.png)  


- Linked Representation


![datastructure-graph-representation-linked-representation3]({{ site.baseurl }}/assets/images/posts/2020/datastructure-graph-representation-linked-representation3.png)  



### 표현
#### Sequential Representation
- 인접 행렬을 사용하여 노드와 edge로 표현 된 매핑을 저장
- 인접 행렬에서 행과 열은 그래프 노드로 표시
- 노드가 n개인 그래프는 nxn 차원

#### Linked Representation   
- 그래프를 컴퓨터의 메모리에 저장하는 데 사용

## 그래프 운행  
### Breath First Search (BFS) 너비우선 탐색
- Queue 인접점 우선
- 모든 인접 노드를 탐색하는 그래프 순회 알고리즘
- 가장 가까운 노드를 선택하고 탐색되지 않은 모든 노드를 탐색
- 모든 노드의 모든 이웃을 탐색하고 각 노드가 정확히 한 번 방문되고 노드가 두 번 방문하지 않음
- 알고리즘은 목표를 찾을 때까지 가장 가까운 각 노드에 대해 동일한 프로세스 따름
- 인접행렬 방식으로 표현한 경우에는 인접 노드 찾는데 O(V) 수행되므로, 시간복잡도 : O(V<sup>2</sup>)
- 인접리스트로 표현한 경우 시간복잡도 : O (V + E) (V :node의 수, E : edge의 수)


[예제보러가기](https://www.javatpoint.com/breadth-first-search-algorithm)


### 예
#### JAVA를 이용한 BFS 구현해보기  

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/graph/bfs/implementation/GraphBFS.java)


### Depth First Search (DFS) 깊이우선 탐색
- Stack 순환호출
- 목표 노드 또는 하위 노드가 없는 노드를 찾을 때까지 더 깊고 깊게 진행
- 데드 엔드에서 아직 완전히 탐색되지 않은 최신 노드로 역 추적
- 프로세스는 BFS 알고리즘과 유사
- 방문하지 않은 노드로 이어지는 가장자리를 검색 가장자리라고 하며, 이미 방문한 노드로 이어지는 가장자리를 블록 가장자리라고 함
- 공간 복잡도 : O (V)  (V :node의 수, E : edge의 수)
- 인접행렬 방식으로 표현한 경우에는 인접 노드 찾는데 O(V) 수행되므로, 시간복잡도 : O(V<sup>2</sup>)
- 인접리스트로 표현한 경우 시간복잡도 : O (V + E) (V :node의 수, E : edge의 수)

[예제보러가기](https://www.javatpoint.com/depth-first-search-algorithm)


### 예
#### JAVA를 이용한 DFS 구현해보기  

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-datastructure/src/graph/bfs/implementation/GraphDFS.java)


## Weight Graph(=network) 가중치 그래프
- 주요문제 : 네트워크 상에 구성된 두 정점간에 가장 최단경로가 무엇인가
- 일반문제 : 네트워크상에서 전체 연결선의 가중치가 최소화 되도록 모든 정점들을 연결하는 것

### Minimal Spanning Tree (MST) : 최소생성 트리
#### Spanning Tree
- 그래프 G에서 연결선 일부를 사용하여 그래프의 모든 정점들이 연결되어 트리로 구성될 때
- 스패닝 트리는 모든 정점을 함께 연결하는 연결 및 무방향 그래프 G의 비순환 하위 그래프
- 그래프 G는 여러 개의 스패닝 트리를 가질수 있음

#### Minimal Spanning Tree
- 가중치 그래프에서 모든 모서리에 가중치를 지정 가능  
- 최소 스패닝 트리는 총 가중치가 최소인 스패닝 트리
- 최소 스패닝 트리는 특정 그래프의 다른 모든 스패닝 트리 중에서 최소 가중치를 포함하는 트리

### 최단 경로 알고리즘
#### Prim's Algorithm (프라임 알고리즘)
#### Kruskal's Algorithm (크루스 칼의 알고리즘)


---
#### references
<https://www.javatpoint.com/ds-graph>  
<https://www.javatpoint.com/graph-representation>  
<https://www.javatpoint.com/spanning-tree>  
<https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/>  
<https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/>  
<https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/>  
<https://www.tutorialspoint.com/data_structures_algorithms/graph_data_structure.htm>  
