---
layout: single
title: "[Problem Solving - Baekjoon] 2606 바이러스"
date: 2020-11-11 23:05:00.000000000 +09:00
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
- baekjoon
- DFS
- BFS
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-2606/"
---
# [Baekjoon Online Judge] 2606 바이러스

## 문제
신종 바이러스인 웜 바이러스는 네트워크를 통해 전파된다. 한 컴퓨터가 웜 바이러스에 걸리면 그 컴퓨터와 네트워크 상에서 연결되어 있는 모든 컴퓨터는 웜 바이러스에 걸리게 된다.

예를 들어 7대의 컴퓨터가 <그림 1>과 같이 네트워크 상에서 연결되어 있다고 하자. 1번 컴퓨터가 웜 바이러스에 걸리면 웜 바이러스는 2번과 5번 컴퓨터를 거쳐 3번과 6번 컴퓨터까지 전파되어 2, 3, 5, 6 네 대의 컴퓨터는 웜 바이러스에 걸리게 된다. 하지만 4번과 7번 컴퓨터는 1번 컴퓨터와 네트워크상에서 연결되어 있지 않기 때문에 영향을 받지 않는다.

### 입력
첫째 줄에는 컴퓨터의 수가 주어진다. 컴퓨터의 수는 100 이하이고 각 컴퓨터에는 1번 부터 차례대로 번호가 매겨진다. 둘째 줄에는 네트워크 상에서 직접 연결되어 있는 컴퓨터 쌍의 수가 주어진다. 이어서 그 수만큼 한 줄에 한 쌍씩 네트워크 상에서 직접 연결되어 있는 컴퓨터의 번호 쌍이 주어진다.

### 출력
1번 컴퓨터가 웜 바이러스에 걸렸을 때, 1번 컴퓨터를 통해 웜 바이러스에 걸리게 되는 컴퓨터의 수를 첫째 줄에 출력한다.

### 예제

- input

```java
7
6
1 2
2 3
1 5
5 2
5 6
4 7
```

- output

```java
4
```

### 분류
- 너비 우선 탐색
- 깊이 우선 탐색

## 풀이

### 문제 파악
- 연결된 노드 갯수를 파악 하면 됨
- dfs나  bfs를 구현하여 방문하는 노드 count만 해주면 됨
- dfs는 구현은 쉬우나 재귀용법이라 많은 노드를 방문할 때 시간초과가 될 수 있으므로 적은 노드를 방문할때 사용.   
- bfs는 구현은 어려우나 많은 노드를 방문할 때 사용

### 구현

### dfs로 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2606/Main.java)

```java
public static void dfs(int[][] adjacent, boolean[] visited, int vertex) {
    visited[vertex] = true;

    for (int i = 1; i < visited.length; i++) {
        if(adjacent[vertex][i] == 1 && !visited[i]) {
            count++;
            dfs(adjacent, visited, i);
        }
    }

}
```

#### bfs 로 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem2606/Main2.java)

```java
public static void bfs(int[][] adjacent, boolean[] visited, int vertex) {
    Queue<Integer> queue = new LinkedList<Integer>();
    queue.add(vertex);

    while(!queue.isEmpty()) {
        int node = queue.poll();

        for (int i = 1; i < visited.length; i++) {
            if (adjacent[node][i] == 1 && !visited[i]) {
                visited[i] = true;
                queue.add(i);
            }
        }
    }
}

```


---
#### references
<https://www.acmicpc.net/problem/2606>
