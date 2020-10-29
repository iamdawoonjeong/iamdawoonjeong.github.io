---
layout: single
title: "[Algorithm] 그래프 순회(Graph Traversal) - BFS, DFS"
date: 2020-08-14 21:54:00.000000000 +09:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Algorithm
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
permalink: "/algorithm-graph-bfs-dfs/"
---
# Graph Traversal (그래프 순회) - BFS, DFS

![algorithm-BFS-and-DFS-Algorithms]({{ site.baseurl }}/assets/images/posts/2020/algorithm-BFS-and-DFS-Algorithms.png)


## Breath First Search (BFS) 너비우선 탐색
- Queue 인접점 우선
- 모든 인접 노드를 탐색하는 그래프 순회 알고리즘
- 가장 가까운 노드를 선택하고 탐색되지 않은 모든 노드를 탐색
- 모든 노드의 모든 이웃을 탐색하고 각 노드가 정확히 한 번 방문되고 노드가 두 번 방문하지 않음
- 알고리즘은 목표를 찾을 때까지 가장 가까운 각 노드에 대해 동일한 프로세스 따름
- 공간 복잡도 : O (V)  (V :node의 수, E : edge의 수)
- 시간복잡도 : O (V + E) (V :node의 수, E : edge의 수)



### JAVA를 이용한 BFS 구현해보기  

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-theory/src/graph/traversal/BFS.java)


## Depth First Search (DFS) 깊이우선 탐색
- Stack 순환호출
- 목표 노드 또는 하위 노드가 없는 노드를 찾을 때까지 더 깊고 깊게 진행
- 데드 엔드에서 아직 완전히 탐색되지 않은 최신 노드로 역 추적
- 프로세스는 BFS 알고리즘과 유사
- 방문하지 않은 노드로 이어지는 가장자리를 검색 가장자리라고 하며, 이미 방문한 노드로 이어지는 가장자리를 블록 가장자리라고 함
- 공간 복잡도 : O (V)  (V :node의 수, E : edge의 수)
- 시간복잡도 : O (V + E) (V :node의 수, E : edge의 수)



### JAVA를 이용한 DFS 구현해보기  

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-theory/src/graph/traversal/DFS.java)


---
#### references
<https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/>  
<https://www.geeksforgeeks.org/depth-first-search-or-dfs-for-a-graph/>  
<https://www.javatpoint.com/breadth-first-search-algorithm>  
<https://www.javatpoint.com/depth-first-search-algorithm>  
<https://www.freelancinggig.com/blog/2019/02/06/what-is-the-difference-between-bfs-and-dfs-algorithms/>
