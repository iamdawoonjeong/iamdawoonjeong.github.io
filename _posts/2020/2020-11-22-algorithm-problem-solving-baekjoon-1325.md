---
layout: single
title: "[Problem Solving - Baekjoon] 1325 효율적인 해킹"
date: 2020-11-22 23:23:00.000000000 +09:00
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
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-1325/"
---
# [Baekjoon Online Judge] 1325 효율적인 해킹

## 문제
해커 김지민은 잘 알려진 어느 회사를 해킹하려고 한다. 이 회사는 N개의 컴퓨터로 이루어져 있다. 김지민은 귀찮기 때문에, 한 번의 해킹으로 여러 개의 컴퓨터를 해킹 할 수 있는 컴퓨터를 해킹하려고 한다.

이 회사의 컴퓨터는 신뢰하는 관계와, 신뢰하지 않는 관계로 이루어져 있는데, A가 B를 신뢰하는 경우에는 B를 해킹하면, A도 해킹할 수 있다는 소리다.

이 회사의 컴퓨터의 신뢰하는 관계가 주어졌을 때, 한 번에 가장 많은 컴퓨터를 해킹할 수 있는 컴퓨터의 번호를 출력하는 프로그램을 작성하시오.

### 입력
첫째 줄에, N과 M이 들어온다. N은 10,000보다 작거나 같은 자연수, M은 100,000보다 작거나 같은 자연수이다. 둘째 줄부터 M개의 줄에 신뢰하는 관계가 A B와 같은 형식으로 들어오며, "A가 B를 신뢰한다"를 의미한다. 컴퓨터는 1번부터 N번까지 번호가 하나씩 매겨져 있다.

### 출력
첫째 줄에, 김지민이 한 번에 가장 많은 컴퓨터를 해킹할 수 있는 컴퓨터의 번호를 오름차순으로 출력한다.

### 예제
- input

```java
5 4
3 1
3 2
4 3
5 3
```

- output

```java
1 2
```

### 분류
- DFS
- BFS

## 풀이

### 문제 파악

- 3 1  : 3이 1를 신뢰한다 ; 1를 해킹하면 3도 해킹 가능
- bfs 방법으로 제일 많은 정점과 연결된 정점을 구하는 문제

```java
5 4
3 1
3 2
4 3
5 3
```


-
### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1325/Main.java)

- 입력된 정점 연결

```java
for (int i = 0; i < m; i++) {
        st = new StringTokenizer(br.readLine());   //A B : A가 B를 신뢰한다 ; B를 해킹하면 A도 해킹 가능
        int a = Integer.parseInt(st.nextToken());
        int b = Integer.parseInt(st.nextToken());
        adjacent[a].add(b);
}
```

- 재귀용법을 사용하는 dfs보다 bfs가 속도면에서 빠르기때문에 bfs 로 구현

```java
public static void bfs(int vertex) {

    Queue<Integer> queue = new LinkedList<Integer>();
    boolean[] visited = new boolean[n+1];
    visited[vertex] = true;
    queue.add(vertex);

    while(!queue.isEmpty()) {
        int value = queue.poll();

        for (int i = 0; i < adjacent[value].size(); i++) {

            int v = adjacent[value].get(i);
            if(!visited[v]) {
                queue.add(v);
                visited[v] = true;
                result[v]++;
            }
        }
    }
}
```

- 반복문에 함께 연산을 넣었더니 시간초과 발생하여 따로 해 줌

```java
for (int i = 1; i < n+1 ; i++) {
    max  = Math.max(max, result[i]);
}

for (int i = 1; i < n+1 ; i++) {
    if (result[i] ==  max) {
      sb.append(i + " ");
    }
}
```


- bfs 연산 돌림

```java
result = new int[n+1];
StringBuilder sb = new StringBuilder();
int max =  0;

for (int i = 1; i < n+1; i++) {
    bfs(i);
}
```

---

#### references
<https://www.acmicpc.net/problem/1325>
