---
layout: single
title: "[Problem Solving - Baekjoon] 1697 숨바꼭질"
date: 2020-11-10 23:10:00.000000000 +09:00
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
permalink: "/algorithm-problem-solving-baekjoon-1697/"
---
# [Baekjoon Online Judge] 1697 숨바꼭질

## 문제
수빈이는 동생과 숨바꼭질을 하고 있다. 수빈이는 현재 점 N(0 ≤ N ≤ 100,000)에 있고, 동생은 점 K(0 ≤ K ≤ 100,000)에 있다. 수빈이는 걷거나 순간이동을 할 수 있다. 만약, 수빈이의 위치가 X일 때 걷는다면 1초 후에 X-1 또는 X+1로 이동하게 된다. 순간이동을 하는 경우에는 1초 후에 2*X의 위치로 이동하게 된다.

수빈이와 동생의 위치가 주어졌을 때, 수빈이가 동생을 찾을 수 있는 가장 빠른 시간이 몇 초 후인지 구하는 프로그램을 작성하시오.

### 입력
첫 번째 줄에 수빈이가 있는 위치 N과 동생이 있는 위치 K가 주어진다. N과 K는 정수이다.

### 출력
수빈이가 동생을 찾는 가장 빠른 시간을 출력한다.

### 예제

- input

```java
5 17
```

- output

```java
4
```

### 분류
- bfs

## 풀이

### 문제 파악

- 기본적인 문제 (많이 풀어봐야 함)
- 시작정점(n) 5 에서 도착정점(k) 17 까지의 시간 구하기

```java
5 17
```

- 위치이동은 X-1, X+1, 2*X
- 방문했던 노드는 또 나오면 안됨

```java
              5
      /       |          \
    4         6          10
 /  |  \   /  |  \    /   |   \
3   5  8  5   7  12  9   11   20
 ```


### 구현

[전체소스보기](https://github.com/iamdawoonjeong/java-datastructure-algorithm/blob/master/java-algorithm-problem-solving/src/baekjoon/problem1697/Main.java)

```java
public static void bfs(int[] adjacent, int start, int end) {

    Queue<Integer> queue= new LinkedList<Integer>();
    queue.add(start);

    while(!queue.isEmpty()) {
        int now = queue.poll();
        if (now == end) {
            break;
        }

       if ( now > 0 && adjacent[now-1] == 0) {
           queue.add(now-1);
           adjacent[now-1] = adjacent[now] + 1;
        }

       if ( now < 100000 && adjacent[now+1] == 0) {
           queue.add(now+1);
           adjacent[now+1] = adjacent[now] + 1;
        }

       if ( now*2 <= 100000 && adjacent[now*2] == 0) {
           queue.add(now*2);
           adjacent[now*2] = adjacent[now] + 1;
        }
    }
}
```

---
#### references
<https://www.acmicpc.net/problem/1697>
