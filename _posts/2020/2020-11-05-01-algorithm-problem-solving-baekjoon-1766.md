---
layout: single
title: "[Problem Solving - Baekjoon] 1766 문제집"
date: 2020-11-05 22:43:00.000000000 +09:00
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
- queue
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-1766/"
---
# [Baekjoon Online Judge] 1766 문제집

## 문제
민오는 1번부터 N번까지 총 N개의 문제로 되어 있는 문제집을 풀려고 한다. 문제는 난이도 순서로 출제되어 있다. 즉 1번 문제가 가장 쉬운 문제이고 N번 문제가 가장 어려운 문제가 된다.

어떤 문제부터 풀까 고민하면서 문제를 훑어보던 민오는, 몇몇 문제들 사이에는 '먼저 푸는 것이 좋은 문제'가 있다는 것을 알게 되었다. 예를 들어 1번 문제를 풀고 나면 4번 문제가 쉽게 풀린다거나 하는 식이다. 민오는 다음의 세 가지 조건에 따라 문제를 풀 순서를 정하기로 하였다.

1. N개의 문제는 모두 풀어야 한다.
2. 먼저 푸는 것이 좋은 문제가 있는 문제는, 먼저 푸는 것이 좋은 문제를 반드시 먼저 풀어야 한다.
3. 가능하면 쉬운 문제부터 풀어야 한다.

예를 들어서 네 개의 문제가 있다고 하자. 4번 문제는 2번 문제보다 먼저 푸는 것이 좋고, 3번 문제는 1번 문제보다 먼저 푸는 것이 좋다고 하자. 만일 4-3-2-1의 순서로 문제를 풀게 되면 조건 1과 조건 2를 만족한다. 하지만 조건 3을 만족하지 않는다. 4보다 3을 충분히 먼저 풀 수 있기 때문이다. 따라서 조건 3을 만족하는 문제를 풀 순서는 3-1-4-2가 된다.

문제의 개수와 먼저 푸는 것이 좋은 문제에 대한 정보가 주어졌을 때, 주어진 조건을 만족하면서 민오가 풀 문제의 순서를 결정해 주는 프로그램을 작성하시오.

### 입력
첫째 줄에 문제의 수 N(1 ≤ N ≤ 32,000)과 먼저 푸는 것이 좋은 문제에 대한 정보의 개수 M(1 ≤ M ≤ 100,000)이 주어진다. 둘째 줄부터 M개의 줄에 걸쳐 두 정수의 순서쌍 A,B가 빈칸을 사이에 두고 주어진다. 이는 A번 문제는 B번 문제보다 먼저 푸는 것이 좋다는 의미이다.

항상 문제를 모두 풀 수 있는 경우만 입력으로 주어진다.

### 출력
첫째 줄에 문제 번호를 나타내는 1 이상 N 이하의 정수들을 민오가 풀어야 하는 순서대로 빈칸을 사이에 두고 출력한다.

### 예제

- input

```java
4 2
4 2
3 1
```

- output

```java
3 1 4 2
```

### 분류
- 우선순위 큐

## 풀이

### 문제 파악
- 위상정렬 문제
- 4번 풀고 2번 풀기 : 4->2
- 3번 풀고 1번 풀기 : 3->1
- 2,1 에 진입차수 1씩 증가
- 4,3은 진입차수가 0이 됨 

```java
4 2 // 4개의 수(n), 2개의 먼저풀어야할 문제 정보의 개수(m)
4 2 // 4번문제는 2번문제보다 먼저 푸는 것이 좋음
3 1
```

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1766/Main.java)

- 배열 및 위상을 입력할 변수 선언

```java
ArrayList<Integer>[] list = new ArrayList[n+1];
for (int i = 0; i <= n; i++) {
    list[i] = new ArrayList<Integer>();
}

int[] indegree  = new int[n+1];
```


- 어떤 문제가 먼저 풀면 좋은지 저장

```java
for (int i = 0; i < m; i++) {
    st = new StringTokenizer(br.readLine());
    int a = Integer.parseInt(st.nextToken());
    int b = Integer.parseInt(st.nextToken());

    //A번 문제는 B번 문제보다 먼저 푸는 것이 좋다는 의미
    list[a].add(b);
    //B번 문제는 간선이 추가됨
    indegree[b] += 1;
}
```

- 진입차수가 0인 노드가 시작 노드임으로 queue에 담기

```java
PriorityQueue<Integer> pq = new PriorityQueue<Integer>();

for (int i = 1; i <= n; i++) {
    //진입차수가 0 -> 시작 노드
    if (indegree[i] == 0) {
        pq.offer(i);
    }
}
```        


- queue 가 빌때까지 연결된 간선체크하면서 뽑기

```java
ArrayList<Integer> result = new ArrayList<Integer>();

while(!pq.isEmpty()) {

    //진입차수가 0인 node 를 먼저 뽑고
    int node = pq.poll();
    result.add(node);

    //해당 node에 연결된 간선 체크
    for (int i = 0; i < list[node].size(); i++) {
        //연결된 노드확인
        int y = list[node].get(i);
        //간선제거
        indegree[y] -= 1;
        if ( indegree[y] == 0) {
            pq.add(y);
        }
    }
}
```

---

#### references
<https://www.acmicpc.net/problem/1766>
