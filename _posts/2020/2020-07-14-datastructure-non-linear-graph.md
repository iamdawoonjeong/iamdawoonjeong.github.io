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
permalink: "/datastructure-non-linear-graph/"
---
# [Data Structure] 비선형 자료구조(2)  - 그래프(Graph)
- 트리(Tree)
- **그래프(Graph)**


## 그래프 Graph
- **vertex와 edge연결선의 집합으로 정의**
- **vertex or node (정점) : 그래프의 각 노드는 정점으로 표시   V = {0,1,2,3,4}**
- **edge or arc (연결선) : 두 정점 사이의 경로 또는 두 정점 사이의 선  E = {01, 12, 23, 34, 04, 14, 13}**
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


#### Weighted Graph(=network) (가중치 그래프)
- 각 모서리에는 길이 또는 무게와 같은 일부 데이터가 할당됨
- edge의 E의 가중치는 w(E)로 주어질 수 있으며, 이는 edge를 순회하는 비용을 나타내는 양수 (+) 값 이여야 함
- Sequential Representation
- 주요문제 : 네트워크 상에 구성된 두 정점간에 가장 최단경로가 무엇인가
- 일반문제 : 네트워크상에서 전체 연결선의 가중치가 최소화 되도록 모든 정점들을 연결하는 것


### 표현
#### Sequential Representation
- 인접 행렬을 사용하여 노드와 edge로 표현 된 매핑을 저장
- 인접 행렬에서 행과 열은 그래프 노드로 표시
- 노드가 n개인 그래프는 nxn 차원


![datasturcture-sequential-representation3]({{ site.baseurl }}/assets/images/posts/2020/datasturcture-sequential-representation3.png)  


#### Linked Representation   
- 그래프를 컴퓨터의 메모리에 저장하는 데 사용


![datastructure-graph-representation-linked-representation3]({{ site.baseurl }}/assets/images/posts/2020/datastructure-graph-representation-linked-representation3.png)  



---
#### references
<https://www.javatpoint.com/ds-graph>  
<https://www.javatpoint.com/graph-representation>  
<https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/>  
<https://www.tutorialspoint.com/data_structures_algorithms/graph_data_structure.htm>  
