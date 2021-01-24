---
layout: single
title: "[Problem Solving - Baekjoon] 1012 유기농 배추"
date: 2020-11-11 23:10:00.000000000 +09:00
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
- flood fill
meta:
  _edit_last: '2'
author:
  login: DawoonJeong
  email: iamdawoonjeong@gmail.com
  display_name: Dawoon Jeong
  first_name: Dawoon
  last_name: Jeong
permalink: "/algorithm-problem-solving-baekjoon-1012/"
---
# [Baekjoon Online Judge] 1012 유기농 배추

## 문제
차세대 영농인 한나는 강원도 고랭지에서 유기농 배추를 재배하기로 하였다. 농약을 쓰지 않고 배추를 재배하려면 배추를 해충으로부터 보호하는 것이 중요하기 때문에, 한나는 해충 방지에 효과적인 배추흰지렁이를 구입하기로 결심한다. 이 지렁이는 배추근처에 서식하며 해충을 잡아 먹음으로써 배추를 보호한다. 특히, 어떤 배추에 배추흰지렁이가 한 마리라도 살고 있으면 이 지렁이는 인접한 다른 배추로 이동할 수 있어, 그 배추들 역시 해충으로부터 보호받을 수 있다.

(한 배추의 상하좌우 네 방향에 다른 배추가 위치한 경우에 서로 인접해있다고 간주한다)

한나가 배추를 재배하는 땅은 고르지 못해서 배추를 군데군데 심어놓았다. 배추들이 모여있는 곳에는 배추흰지렁이가 한 마리만 있으면 되므로 서로 인접해있는 배추들이 몇 군데에 퍼져있는지 조사하면 총 몇 마리의 지렁이가 필요한지 알 수 있다.

예를 들어 배추밭이 아래와 같이 구성되어 있으면 최소 5마리의 배추흰지렁이가 필요하다.

(0은 배추가 심어져 있지 않은 땅이고, 1은 배추가 심어져 있는 땅을 나타낸다.)

### 입력
입력의 첫 줄에는 테스트 케이스의 개수 T가 주어진다. 그 다음 줄부터 각각의 테스트 케이스에 대해 첫째 줄에는 배추를 심은 배추밭의 가로길이 M(1 ≤ M ≤ 50)과 세로길이 N(1 ≤ N ≤ 50), 그리고 배추가 심어져 있는 위치의 개수 K(1 ≤ K ≤ 2500)이 주어진다. 그 다음 K줄에는 배추의 위치 X(0 ≤ X ≤ M-1), Y(0 ≤ Y ≤ N-1)가 주어진다.

### 출력
각 테스트 케이스에 대해 필요한 최소의 배추흰지렁이 마리 수를 출력한다.

### 예제1

- input

```java
2
10 8 17
0 0
1 0
1 1
4 2
4 3
4 5
2 4
3 4
7 4
8 4
9 4
7 5
8 5
9 5
7 6
8 6
9 6
10 10 1
5 5
```

- output

```java
5
1
```

### 예제2

- input

```java
1
5 3 6
0 2
1 2
2 2
3 2
4 2
4 0
```

- output

```java
2
```

### 분류
- 너비 우선 탐색(bfs)
- 깊이 우선 탐색(dfs)

## 풀이

### 문제 파악
- 연결되어있는 점들의 집합군의 갯수를 구하는 dfs, bfs문제
- flood fill 문제

### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1012/Main.java)


- 인접 좌표들를 확인하는 dfs메소드를 한번 탈때마다 count 해줘서 그 값을 출력 해주면 됨

```java
for (int i = 0; i < testCase; i++) {
    StringTokenizer st = new StringTokenizer(br.readLine());
    m = Integer.parseInt(st.nextToken());
    n = Integer.parseInt(st.nextToken());
    int k = Integer.parseInt(st.nextToken());

    int[][] adjacent  = new int[m][n];
    for (int j = 0; j < k; j++) {
        st = new StringTokenizer(br.readLine());

        int x = Integer.parseInt(st.nextToken());
        int y = Integer.parseInt(st.nextToken());
        adjacent[x][y] = 1;
    }

    int result = 0;
    boolean[][] visited = new boolean[m][n];
    for (int p = 0; p < m; p++) {
        for (int q = 0; q < n; q++) {
            if (adjacent[p][q] == 1 && !visited[p][q]) {
                dfs(adjacent, visited, p, q);
                result++;
            }
        }
    }
    System.out.println(result);
}
```

- 상하좌우 인접행렬의 좌표값이 1 인 값들을 모두 확인하여 방문여부를 체크해야 나중에 또 방문 안 함

```java
private static void dfs(int[][] adjacent, boolean[][] visited, int x, int y) {

    visited[x][y] = true;
    int[][] directions = new int[][] { { -1 , 0 }, { 1 , 0 }, { 0 , -1 }, { 0 , 1 }  } ;

    for (int[] is : directions) {
        int nextX = x+is[0];
        int nextY = y+is[1];

        if (nextX < 0 || nextX >= m || nextY < 0 || nextY >= n ) {
            continue;
        }

        if (adjacent[nextX][nextY] == 1 && !visited[nextX][nextY]) {
            dfs(adjacent, visited, nextX, nextY);
        }
    }
}
```

---
#### references
<https://www.acmicpc.net/problem/1012>
