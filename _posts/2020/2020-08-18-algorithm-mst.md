---
layout: single
title: "[Algorithm] Minimum Spanning Tree (MST: 최소신장트리)"
date: 2020-08-18 21:04:00.000000000 +09:00
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
permalink: "/algorithm-mst/"
---
# Minimum Spanning Tree (MST: 최소신장트리)

## Spanning Tree 속성
- 최소 가장자리 수를 갖는 동일한 가중치의 최소 스패닝 트리가 여러 개 존재 가능
- 주어진 그래프의 모든 간선 가중치가 동일하면 해당 그래프의 모든 스패닝 트리가 최소
- 각 모서리에 고유 한 가중치가있는 경우 고유 한 최소 스패닝 트리가 하나만 있음
- 연결된 그래프 G는 하나 이상의 스패닝 트리를 가질 수 있음
- 연결이 끊어진 그래프는 트리에 걸쳐있을 필요가 없거나 모든 정점에 걸쳐있을 수 없음
- 스패닝 트리에는 주기가 없음
- 스패닝 트리에는 (n-1) 개의 가장자리가 있는데,  여기서 n은 정점의 수
- 단일 에지를 하나만 추가하면 스패닝 트리가 비순환 성 속성을 잃고 하나의 단일 에지를 제거하면 연결 속성이 손실되어짐


![algorithm-introduction-of-minimum-spanning-tree4]({{ site.baseurl }}/assets/images/posts/2020/algorithm-introduction-of-minimum-spanning-tree4.png)


## Minimum Spanning Tree
- 최소 스패닝 트리는 최소 총 비용이 있는 스패닝 트리
- 가중치 (또는 비용)가있는 링크 된 무 방향 그래프가 각 모서리와 결합 된 경우.
- **스패닝 트리의 비용은 가장자리 비용의 합계**
- **사이클이 형성되면 안 됨**
- 실제 상황에서이 가중치는 거리, 혼잡, 교통 부하 또는 가장자리에 표시된 임의의 값으로 측정

![algorithm-introduction-of-minimum-spanning-tree5]({{ site.baseurl }}/assets/images/posts/2020/algorithm-introduction-of-minimum-spanning-tree5.png)
![algorithm-introduction-of-minimum-spanning-tree6]({{ site.baseurl }}/assets/images/posts/2020/algorithm-introduction-of-minimum-spanning-tree6.png)

### 대표적인 MST 알고리즘
- **Kruscal's algoritm**
- **Prim algorithm**

---

#### references
<https://www.javatpoint.com/minimum-spanning-tree-introduction>  
<https://www.geeksforgeeks.org/applications-of-minimum-spanning-tree/>  
<https://www.tutorialspoint.com/data_structures_algorithms/spanning_tree.htm>  
