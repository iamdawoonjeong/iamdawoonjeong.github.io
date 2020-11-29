---
layout: single
title: "[Problem Solving - Baekjoon] 1774 우주신과의 교감"
date: 2020-11-26 22:00:00.000000000 +09:00
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
- mst
- kruskal
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-1774/"
---
# [Baekjoon Online Judge] 1774 우주신과의 교감

## 문제
황선자씨는 우주신과 교감을 할수 있는 채널러 이다. 하지만 우주신은 하나만 있는 것이 아니기때문에 황선자 씨는 매번 여럿의 우주신과 교감하느라 힘이 든다. 이러던 와중에 새로운 우주신들이 황선자씨를 이용하게 되었다.

하지만 위대한 우주신들은 바로 황선자씨와 연결될 필요가 없다. 이미 황선자씨와 혹은 이미 우주신끼리 교감할 수 있는 우주신들이 있기 때문에 새로운 우주신들은 그 우주신들을 거쳐서 황선자 씨와 교감을 할 수 있다.

우주신들과의 교감은 우주신들과 황선자씨 혹은 우주신들 끼리 이어진 정신적인 통로를 통해 이루어 진다. 하지만 우주신들과 교감하는 것은 힘든 일이기 때문에 황선자씨는 이런 통로들이 긴 것을  좋아하지 않는다. 왜냐하면 통로들이 길 수록 더 힘이 들기 때문이다.

또한 우리들은 3차원 좌표계로 나타낼 수 있는 세상에 살고 있지만 우주신들과 황선자씨는 2차원 좌표계로 나타낼 수 있는 세상에 살고 있다. 통로들의 길이는 2차원 좌표계상의 거리와 같다.

이미 황선자씨와 연결된, 혹은 우주신들과 연결된 통로들이 존재한다. 우리는 황선자 씨를 도와 아직 연결이 되지 않은 우주신들을 연결해 드려야 한다. 새로 만들어야 할 정신적인 통로의 길이들이 합이 최소가 되게 통로를 만들어 “빵상”을 외칠수 있게 도와주자.

### 입력
첫째 줄에 우주신들의 개수(N<=1,000) 이미 연결된 신들과의 통로의 개수(M<=1,000)가 주어진다.

두 번째 줄부터 N개의 줄에는 황선자를 포함하여 우주신들의 좌표가 (0<= X<=1,000,000), (0<=Y<=1,000,000)가 주어진다. 그 밑으로 M개의 줄에는 이미 연결된 통로가 주어진다. 번호는 위의 입력받은 좌표들의 순서라고 생각하면 된다. 좌표는 정수이다.

### 출력
첫째 줄에 만들어야 할 최소의 통로 길이를 출력하라. 출력은 소수점 둘째짜리까지 출력하여라.

### 예제
- input

```java
4 1
1 1
3 1
2 3
4 3
1 4
```

- output

```java
4.00
```

### 힌트
(1,1) (3,1) (2,3) (4,3) 이렇게 우주신들과 황선자씨의 좌표가 주어졌고 1번하고 4번이 연결되어 있다. 그렇다면 1번하고 2번을 잇는 통로를 만들고 3번하고 4번을 잇는 통로를 만들면 신들과 선자씨끼리 다 도달이 가능하면서 더 만들어야 할 통로의 길이는 최소가 된다.

### 분류
- 최소 스패닝 트리

## 풀이

### 문제 파악
- 좌표 정보로 알려주니 이를 노드와 가중치 정보 getDistance() 로 환산해줄 함수 필요
- 최소 스패닝 트리중 크루스칼 문제
- 모든 node를 가중치 오름차순으로 정렬 Collectinos.sort()
- 가중치가 가장 작은 node를 선택하여 지금까지 형성된 트리 정보와 함께 사이클이 형성 되는지 확인 : 연결된 노드의 부모가 같은지 확인 find()
- 사이클이 형성 되지 않는 경우, 연결 시켜 주기 :  부모가 같지 않다면, 연결 시켜주기 union()
- 모든 연결 선의 가중치를 합해서 출력

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1774/Main.java)


- 좌표간 거리 계산 : (x1-x2)<sup>2</sup> - (y1-y2)<sup>2</sup> 이 root 값

```java
public static double getDistance(Location p1, Location p2) {
    double a = Math.abs(p1.x - p2.x);
    double b = Math.abs(p1.y - p2.y);

    //sqrt :  square root
    return Math.sqrt((a*a)+(b*b));
}
```

- union  : 두개의 집합의 부모를 찾아 같지 않다면 서로 싸이클이 생기지 않으므로 합쳐 줌

```java
private static void union(int a, int b) {
    //합치기 전에  find 함수를 수행해서 두개의 부모가 같은지 확인
    a = find(a);
    b = find(b);

    // 부모가 같지 않다면 입력
    if ( a != b) {
        parent[b] = a;
    }

}

```

- find : 각 노드 집합의 부모를 찾아 반환

```java
private static int find(int a) {
    if ( a == parent[a]) {
        return a;
    }

    return parent[a] = find(parent[a]);
}
```

- 노드 클래스

```java
class Node implements Comparable<Node>{
    public int src, dest;
    public double weight;

    Node(int src, int dest, double weight) {
        this.src = src;
        this.dest = dest;
        this.weight = weight;
    }

    public int compareTo(Node o) {
        if (weight < o.weight) {
            return -1;
        }
        return 1;
    }
}
```


- 좌표 클래스

```java
class Location{
    int index;
    double x, y;

    Location(int index, double x, double y){
        this.index = index;
        this.x = x;
        this.y = y;
    }

}
```

- 좌표 정보 받아 좌표 생성

```java
Location[] location = new Location[n+1];

for (int i = 1; i < n+1; i++) {
    st = new StringTokenizer(br.readLine());
    double x = Integer.parseInt(st.nextToken());
    double y = Integer.parseInt(st.nextToken());
    location[i] = new Location(i, x, y);
}
```

- 입력된 좌표로 거리 구하고 Node 생성

```java
adjacent = new ArrayList<>();

for (int i = 1; i < n+1; i++) {
    for (int j = i+1; j < n+1; j++) {
        adjacent.add(new Node(location[i].index, location[j].index, getDistance( location[i],  location[j]))) ;
    }
}
```

- 부모정보를 입력 : union 가능한지 체크할 때 사용

```java
parent = new int[n+1];

for (int i = 1; i < n+1; i++) {
    parent[i] = i;
}
```

- 주어진 간선 정보를 연결 : union 으로 부모가 같은지 확인 후 입력

```java
for (int i = 0; i < m; i++) {
    st = new StringTokenizer(br.readLine());
    int a = Integer.parseInt(st.nextToken());
    int b = Integer.parseInt(st.nextToken());
    union(a, b);
}
```

- 노드 간의 비용 순으로 정렬 (크루스칼 알고리즘은 모든 정점의 최소 간선정보 순으로 연결)

```java
Collections.sort(adjacent);
```

- 크루스칼 알고리즘 : 가중치기준으로 오름차순된 노드를 하나씩 탐색하면서,  연결 할 두 노드의 부모가 같지 않다면(find) 연결 해주고(union) 해당 연결선의 가중치의 합을 구함  

```java
for (Node  node : adjacent) {
    if (find(node.src) != find(node.dest)) {
        union(node.src, node.dest);
        result += node.weight;
    }
}
```

- 소수점 둘째 자리 까지 출력 String.format() 사용

```java
System.out.println(String.format("%.2f", result));
```

---
#### references
<https://www.acmicpc.net/problem/1774>
