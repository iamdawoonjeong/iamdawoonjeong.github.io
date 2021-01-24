---
layout: single
title: "[Problem Solving - Baekjoon] 1260 DFS와 BFS"
date: 2020-11-10 23:05:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-1260/"
---
# [Baekjoon Online Judge] 1260 DFS와 BFS

## 문제
그래프를 DFS로 탐색한 결과와 BFS로 탐색한 결과를 출력하는 프로그램을 작성하시오. 단, 방문할 수 있는 정점이 여러 개인 경우에는 정점 번호가 작은 것을 먼저 방문하고, 더 이상 방문할 수 있는 점이 없는 경우 종료한다. 정점 번호는 1번부터 N번까지이다.

### 입력
첫째 줄에 정점의 개수 N(1 ≤ N ≤ 1,000), 간선의 개수 M(1 ≤ M ≤ 10,000), 탐색을 시작할 정점의 번호 V가 주어진다. 다음 M개의 줄에는 간선이 연결하는 두 정점의 번호가 주어진다. 어떤 두 정점 사이에 여러 개의 간선이 있을 수 있다. 입력으로 주어지는 간선은 양방향이다.

### 출력
첫째 줄에 DFS를 수행한 결과를, 그 다음 줄에는 BFS를 수행한 결과를 출력한다. V부터 방문된 점을 순서대로 출력하면 된다.

### 예제1
- input

```java
4 5 1
1 2
1 3
1 4
2 4
3 4
```

- output

```java
1 2 4 3
1 2 3 4
```

### 예제2
- input

```java
5 5 3
5 4
5 2
1 2
3 4
3 1
```

- output

```java
3 1 2 5 4
3 1 4 2 5
```

### 예제3
- input

```java
1000 1 1000
999 1000
```

- output

```java
1000 999
1000 999
```
### 분류


## 풀이

### 문제 파악
- **dfs와 bfs를 구현하는 가장 기본 적인 문제**

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1260/Main.java)

- dfs : 재귀용법으로 풀이

```java
public static void dfs(int[][] adjacent, boolean[] visited, int vertex) {

    visited[vertex] = true;
    System.out.print(vertex + " ");

    for (int i = 1; i < visited.length; i++) {
        if(adjacent[vertex][i] == 1 && !visited[i]) {
            dfs(adjacent, visited, i);
        }
    }
}
```

- bfs

```java
public static void bfs(int[][] adjacent, boolean[] visited, int vertex) {
    Queue<Integer> queue = new LinkedList<Integer>();

    visited[vertex] = true;
    queue.add(vertex);

    while(!queue.isEmpty()) {
        vertex = queue.poll();
        System.out.print( vertex + " ");

        for (int i = 1; i < visited.length; i++) {
            if(adjacent[vertex][i] == 1 && !visited[i]) {
                queue.add(i);
                visited[i] = true;
            }
        }
    }
}
```

---
#### references
<https://www.acmicpc.net/problem/1260>
