---
layout: single
title: "[Algorithm] 최소신장트리 (MST) - 크루스칼(Kruscal), 프림(Prim)"
date: 2020-08-17 21:04:00.000000000 +09:00
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
- tree
- MST
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
- 최소 가장자리 수를 갖는 동일한 가중치의 **Minimum Spanning Tree**가 여러 개 존재 가능
- 주어진 그래프의 모든 간선 가중치가 동일하면 해당 그래프의 모든 스패닝 트리가 최소
- 각 모서리에 고유 한 가중치가있는 경우 고유 한 최소 스패닝 트리가 하나만 있음
- 연결된 그래프 G는 하나 이상의 스패닝 트리를 가질 수 있음
- 연결이 끊어진 그래프는 트리에 걸쳐있을 필요가 없거나 모든 정점에 걸쳐있을 수 없음
- 스패닝 트리에는 주기가 없음
- 스패닝 트리에는 (n-1) 개의 가장자리가 있는데,  여기서 n은 정점의 수
- 단일 에지를 하나만 추가하면 스패닝 트리가 비순환 성 속성을 잃고 하나의 단일 에지를 제거하면 연결 속성이 손실되어짐
- 그래프 G에서 연결선 일부를 사용하여 그래프의 모든 정점들이 연결되어 트리로 구성될 때
- 스패닝 트리는 모든 정점을 함께 연결하는 연결 및 무방향 그래프 G의 비순환 하위 그래프
- 그래프 G는 여러 개의 스패닝 트리를 가질수 있음

![algorithm-introduction-of-minimum-spanning-tree4]({{ site.baseurl }}/assets/images/posts/2020/algorithm-introduction-of-minimum-spanning-tree4.png)


## Minimal Spanning Tree (MST) : 최소생성 트리
- 최소 스패닝 트리는 최소 총 비용이 있는 스패닝 트리
- 가중치 (또는 비용)가있는 링크 된 무 방향 그래프가 각 모서리와 결합 된 경우.
- **스패닝 트리의 비용은 가장자리 비용의 합계**
- **사이클이 형성되면 안 됨**
- 실제 상황에서이 가중치는 거리, 혼잡, 교통 부하 또는 가장자리에 표시된 임의의 값으로 측정
- 가중치 그래프에서 모든 모서리에 가중치를 지정 가능  
- 최소 스패닝 트리는 총 가중치가 최소인 스패닝 트리
- 최소 스패닝 트리는 특정 그래프의 다른 모든 스패닝 트리 중에서 최소 가중치를 포함하는 트리


![algorithm-introduction-of-minimum-spanning-tree5]({{ site.baseurl }}/assets/images/posts/2020/algorithm-introduction-of-minimum-spanning-tree5.png)


![algorithm-introduction-of-minimum-spanning-tree6]({{ site.baseurl }}/assets/images/posts/2020/algorithm-introduction-of-minimum-spanning-tree6.png)


### 대표적인 MST 알고리즘 종류
- **Kruscal's algoritm(크루스 칼의 알고리즘)**
- **Prim algorithm(프라임 알고리즘)**




## Union-Find algorithm (유니온-파인드 알고리즘)
- Disjoint Set 만들기
- Union -
- Find - 싸이클이 안 생기는 edge 찾기. 싸이클이 생기면 버리기


### union-by-rank 기법
- rank가 다른 트리가 붙을 때
- rank가 같은 트리가 붙을 때


## **Kruscal's algoritm (크루스 칼의 알고리즘)**
- 최적의 솔루션을 찾는 탐욕스러운 접근 방식
- 연결된 그래프와 무 방향 그래프가 주어지면 해당 그래프의 스패닝 트리는 트리이고 모든 정점을 함께 연결하는 하위 그래프
- 스패닝 트리의 가중치는 스패닝 트리의 각 가장자리에 지정된 가중치의 합계
- 시간복잡도 : O (ElogE) 또는 O (ElogV)




### 연산
1. 오름차순으로 모든 edge 정렬
2. 가장 작은 edge를 선택 후, 지금까지 형성된 스패닝 트리와 함께 사이클을 형성하는지 확인
3. 사이클이 형성되지 않은 경우, edge 포함시키고 그렇지 않은 경우에는 edge 버리기
3. 스패닝 트리에 (V-1) 가장자리가 있을 때까지 2-3단계를 반복



![algorithm-Fig-0-300x139]({{ site.baseurl }}/assets/images/posts/algorithm-Fig-0-300x139.jpg)


![algorithm-fig8new]({{ site.baseurl }}/assets/images/posts/algorithm-fig8new.jpeg)



### 자바를 이용하여 MST - Kruskal algorithm 구현

[전체소스보기]()


```java

```



output

```
```



---

#### references
<https://www.javatpoint.com/minimum-spanning-tree-introduction>  
<https://www.javatpoint.com/kruskals-minimum-spanning-tree-algorithm>  
<https://www.javatpoint.com/kruskal-algorithm>  
<https://www.geeksforgeeks.org/applications-of-minimum-spanning-tree/>  
<https://www.geeksforgeeks.org/kruskals-minimum-spanning-tree-algorithm-greedy-algo-2/?ref=lbp>
<https://www.tutorialspoint.com/data_structures_algorithms/spanning_tree.htm>   
