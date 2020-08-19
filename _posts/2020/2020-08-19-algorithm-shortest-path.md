---
layout: single
title: "[Algorithm] Shortest Path (최단경로)"
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
# Shortest Path (최단경로)

## Dijkstra의 알고리즘
- 최단 경로 문제를 해결하는 greedy algorithm
- MST(Minimum Spanning Tree) 대한 Prim algorithm 과 매우 유사합
- 주어진 소스를 루트로 사용하여 SPT (최단 경로 트리) 를 생성
- "가장 가벼운"또는 "가장 가까운" 꼭지점을 선택하여 집합 S에 삽입하기 때문에 greedy strategy

![algorithm-dijkstra]({{ site.baseurl }}/assets/images/posts/2020/algorithm-dijkstra.png)

![algorithm-dijkstra7]({{ site.baseurl }}/assets/images/posts/2020/algorithm-dijkstra7.png)

### Dijkstra 알고리즘의 단점
- 블라인드 검색을 수행하므로 처리하는 동안 많은 시간을 낭비
- 음의 가장자리를 처리 못 함
- 비순환 그래프로 이어지며 가장 자주 올바른 최단 경로를 얻을 수 없음  
- 방문한 정점을 추적을 해야 함


---

#### references
<https://www.javatpoint.com/dijkstras-algorithm>  
<https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/>
<https://www.tutorialspoint.com/design_and_analysis_of_algorithms/design_and_analysis_of_algorithms_shortest_paths.htm>    
