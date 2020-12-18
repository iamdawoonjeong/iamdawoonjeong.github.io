---
layout: single
title: "[Problem Solving - Baekjoon] 10282 해킹"
date: 2020-11-24 18:50:00.000000000 +09:00
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
- dijkstra
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-10282/"
---
# [Baekjoon Online Judge] 10282 해킹

## 문제
최흉최악의 해커 yum3이 네트워크 시설의 한 컴퓨터를 해킹했다! 이제 서로에 의존하는 컴퓨터들은 점차 하나둘 전염되기 시작한다. 어떤 컴퓨터 a가 다른 컴퓨터 b에 의존한다면, b가 감염되면 그로부터 일정 시간 뒤 a도 감염되고 만다. 이때 b가 a를 의존하지 않는다면, a가 감염되더라도 b는 안전하다.

최흉최악의 해커 yum3이 해킹한 컴퓨터 번호와 각 의존성이 주어질 때, 해킹당한 컴퓨터까지 포함하여 총 몇 대의 컴퓨터가 감염되며 그에 걸리는 시간이 얼마인지 구하는 프로그램을 작성하시오.

### 입력
첫째 줄에 테스트 케이스의 개수가 주어진다. 테스트 케이스의 개수는 최대 100개이다. 각 테스트 케이스는 다음과 같이 이루어져 있다.

- 첫째 줄에 컴퓨터 개수 n, 의존성 개수 d, 해킹당한 컴퓨터의 번호 c가 주어진다(1 ≤ n ≤ 10,000, 1 ≤ d ≤ 100,000, 1 ≤ c ≤ n).
- 이어서 d개의 줄에 각 의존성을 나타내는 정수 a, b, s가 주어진다(1 ≤ a, b ≤ n, a ≠ b, 0 ≤ s ≤ 1,000). 이는 컴퓨터 a가 컴퓨터 b를 의존하며, 컴퓨터 b가 감염되면 s초 후 컴퓨터 a도 감염됨을 뜻한다.

각 테스트 케이스에서 같은 의존성 (a, b)가 두 번 이상 존재하지 않는다.

### 출력
**각 테스트 케이스마다 한 줄에 걸쳐 총 감염되는 컴퓨터 수, 마지막 컴퓨터가 감염되기까지 걸리는 시간을 공백으로 구분지어 출력한다.**

### 예제

- input

```java
2
3 2 2
2 1 5
3 2 5
3 3 1
2 1 2
3 1 8
3 2 4
```

- output

```java
2 5
3 6
```

### 분류
- 다익스트라

## 풀이

### 문제 파악

- 최단경로를 찾는 다익스트라문제
- 기본 문제라는데, 어려움

```java
2      //2개의 문제
3 2 2  //3개의정점, 2개의 edge, 정점 2에서 시작
2 1 5  //1번 노드 -> 2번 노드 : 가중치가 5
3 2 5
3 3 1
2 1 2
3 1 8
3 2 4
```

#### 첫번째 케이스 : node 2 에서 시작해서 2, 3 컴퓨터 2대를 감염시키고 걸리는 시간은 5

```java
           2
    (5)  ↙︎   ↖︎  (5)
        3      1
```

- adjacent[]

| adjacent    | dest | cost |
|:----:|:----:|:----:|
| adjacent[1] | 2 | 5 |
| adjacent[2] | 3 | 5 |
| adjacent[3] | 3 | 5 |


- distance[]

| 1	| 2 | 3 |
|:----:|:----:|:----:|
| INF | INF | INF |
| INF | 0 | INF |
| INF | 0 | 5 |


#### 두번째 케이스

 : node 1  에서 시작해서, 1, 2, 3 컴퓨터 3대를 감염시키고 걸리는 시간은 6


 ```java
            1
     (2)  ↙︎   ↖︎  (8)
         2  →  3
           (4)
 ```

 - adjacent[]

 | adjacent    | dest | cost |
 |:----:|:----:|:----:|
 | adjacent[1] | 2 | 2 |
 | adjacent[2] | 3 | 4 |
 | adjacent[3] | 1 | 8 |


 - distance[]

| 1	| 2 | 3 |
|:----:|:----:|:----:|
| INF | INF | INF |
| 0 | INF | INF |
| 0 | 2 | INF |
| 0 | 2 | 6 |

- 시작노드에서 최적의 경로로 이동 시 지나가는 노드의 갯수와 가중치를 구하는 문제

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem10282/Main.java)

- 노드에서 연결된 노드와 가중치를 관리 할 Node class 를 만들어 주어서 관리

```java
public static class Node implements Comparable<Node>{
    private int index;
    private int cost;

    public Node(int index, int cost){
        this.index = index;
        this.cost = cost;
    }

    @Override
    public int compareTo(Node o) {
        return this.cost - o.cost;
    }
}
```

- 주어진 testCase만큼 반복

```java
for (int i = 0; i < testCase; i++) {
    StringTokenizer st = new StringTokenizer(br.readLine());
    int n = Integer.parseInt(st.nextToken()); // 컴퓨터 개수 n : node
    int d = Integer.parseInt(st.nextToken()); // 의존성 개수 d : edge
    int c = Integer.parseInt(st.nextToken()); // 해킹당한 컴퓨터의 번호 c :star node

    adjacent = new ArrayList[n+1];

    for (int j = 1; j < n+1; j++) {
        adjacent[j] = new ArrayList<>();
    }

    distance =  new int[n+1];
    Arrays.fill(distance, INF);  //dijkstra는 INF로 채워주고 시작
    count = 1;

    for (int j = 0; j < d; j++) {
        st = new StringTokenizer(br.readLine());
        int a = Integer.parseInt(st.nextToken());  // 컴퓨터 a가 : from
        int b = Integer.parseInt(st.nextToken());  // 컴퓨터 b를 의존  : to
        int s = Integer.parseInt(st.nextToken());  // 컴퓨터 b가 감염되면, s초 후 컴퓨터 a도 감염됨 : weight
        adjacent[b].add(new Node(a,s));
    }

    dijkstra(c);

    ArrayList<Integer> result = new ArrayList<Integer>();
    for (int element : distance) {
        if (element != INF) {
            result.add(element);
        }
    }
    Collections.sort(result);
    System.out.println(count + " " + result.get(result.size()-1));
}
```

- dijksatra는 PriorityQueue를 이용하여 구현
- 시작노드는 0으로 set 해주고 시작

```java
public static void dijkstra(int start){
    PriorityQueue<Node> pq = new PriorityQueue<>();

    distance[start] = 0;
    pq.offer(new Node(start, distance[start]));

    while(!pq.isEmpty()) {
        Node from = pq.poll();

        if (from.cost > distance[from.index]) {
            continue;
        }

        for (Node to : adjacent[from.index]) {
            if (distance[to.index] > distance[from.index] + to.cost) {
                if (distance[to.index] == INF) {
                    count++;
                }
                distance[to.index] = distance[from.index] + to.cost;
                pq.offer(new Node(to.index, distance[to.index]));
            }
        }

    }

}
```

---

#### references
<https://www.acmicpc.net/problem/10282>
