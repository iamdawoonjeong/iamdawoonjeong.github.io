---
layout: single
title: "[Algorithm] 최단경로 (Shortest Path) - 다익스트라(Dijkstra)"
date: 2020-08-19 22:08:00.000000000 +09:00
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
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-shortest-path/"
---
# Shortest Path (최단 경로 알고리즘)

## 최단 경로 알고리즘
- 가중치 그래프(Weighted Graph)에서 한 정점에서 다른 정점으로 갈때, 가중치 합이 최소가 되도로 하는 경로를 찾는 알고리즘
- G = (V, E)

## 최단 경로 알고리즘 종류

### Single - source shortest path problem (단일 출발 최단 경로 문제)
- 주어진 정점 u에서 가장 짧은 경로를 찾아야하는 문제

### Single - destination shortest paths problem (단일 도착 최단 경로 문제)
- 모든 정점에서 주어진 목적지 정점 v까지의 최단 경로를 찾는 문제
- 그래프에서 각 모서리의 방향을 이동하여 이 문제를 single - source problem(단일 출발 문제) 으로 단축 가능

###  All - pairs shortest paths problem (전체 쌍 최단 경로 문제)
- 모든 정점 (u, v) 쌍에 대해 u에서 v까지의 최단 경로를 찾는 문제
- 각 정점에서 한 번만 single - source algorithm(단일 출발 알고리즘)을 실행하면이 문제를 명확히 할 수 있음


## Dijkstra 알고리즘
- Single - source shortest path problem (단일 출발 최단 경로 문제)
- Graph 알고리즘
- "가장 가벼운"또는 "가장 가까운" 꼭지점을 선택하여 최단경로문제를 해결하는 greedy algorithm
- MST(Minimum Spanning Tree) 대한 Prim algorithm 과 매우 유사
- 너비 우선탐색(BFS)와 유사
- 주어진 소스를 루트로 사용하여 SPT (최단 경로 트리) 를 생성


![algorithm-dijkstra]({{ site.baseurl }}/assets/images/posts/2020/algorithm-dijkstra.png)

![algorithm-dijkstra7]({{ site.baseurl }}/assets/images/posts/2020/algorithm-dijkstra7.png)

### Dijkstra 알고리즘의 단점
- 블라인드 검색을 수행하므로 처리하는 동안 많은 시간을 낭비
- 음의 가장자리를 처리 못 함
- 비순환 그래프로 이어지며 가장 자주 올바른 최단 경로를 얻을 수 없음  
- 방문한 정점을 추적을 해야 함

### 연산
1. 각 정점위 위에 시작 점으로 부터 자신에게 이르는 경로의 길이를 무한대로 초기화
2. 시작 정점의 경로길이를 0으로 초기화 하고 최단 경로에 추가



---
#### references
<https://en.wikipedia.org/wiki/Shortest_path_problem>  
<https://www.javatpoint.com/single-source-shortest-paths>  
<https://www.javatpoint.com/dijkstras-algorithm>  
<https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/>
<https://www.tutorialspoint.com/design_and_analysis_of_algorithms/design_and_analysis_of_algorithms_shortest_paths.htm>    
